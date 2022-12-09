# **Subscriptions**

GraphQL은 query와 mutation 외에도 **subscriptions**을 지원한다.

쿼리와 마찬가지로 구독을 통해 데이터를 가져올 수 있다. 쿼리와 달리 구독은 시간이 지남에 따라 결과가 변경될 수 있는 오래 지속되는 작업이다. 이것은 GraphQL서버(보편적으로 webSocket을 통해)에 대한 활성 연결을 유지하여 서버가 구독 결과에 대한 업데이트를 푸시할 수 있도록 한다.

구독은 새 객체 생성 또는 중요한 필드 업데이트와 같은 백엔드 데이터의 변경 사항에 대해 클라이언트에게 실시간으로 알리는데 유용하다.

### subscription을 사용하는 경우

단순히 백엔드를 최신 상태로 유지하기 위해 subscription을 사용해서는 안된다.

다음과 같은 경우 구독을 사용해야 한다.

- **큰 객체에 대한 작은 증분 변경.** 큰 객체에 대한 반복 폴링은 특히 대부분의 객체 필드가 거의 변경되지 않는 경우 비용이 많이 든다. 대신 쿼리를 사용하여 객체의 초기 상태를 가져올 수 있으며 서버는 업데이트가 발생할 때마다 개별 필드에 업데이트를 사전에 푸시할 수 있다.
- **대기 시간이 짧은 실시간 업데이트**. 예를 들어, 채팅 어플리케이션의 클라이언트는 새 메시지를 사용할 수 있게 되는 즉시 받기를 원할 때

## subscription정의

### server측

GraphQL 스키마에서 사용 가능한 구독을 subscription 유형의 필르도 정의한다. 다음 commentAdded 구독은 특정 블로그 게시물에 새 댓글이 추가될 때마다 구독 클라이언트에게 알림이 간다.

```graphql
type Subscription {
  commentAdded(postID: ID!): Comment
}
```

### client측

애플리케이션의 클라이언트에서 다음과 같이 Apollo 클라이언트가 실행할 각 구독의 모양을 정의한다.

```graphql
const COMMENTS_SUBSCRIPTION = gql`
  subscription OnCommentAdded($postID: ID!) {
    commentAdded(postID: $postID) {
      id
      content
    }
  }
`;
```

Apollo 클라이언트는 onCommentAdded 구독을 실행할 때 GraphQL 서버에 대한 연결을 설정하고 응답 데이터를 수신한다. 쿼리와 달리 서버가 즉시 처리하고 응답을 반환할 것이라는 기대는 없다. 대신, 백엔드에서 특정 이벤트가 발생할 때만 서버가 클라이언트에 데이터를 푸시한다.

GraphQL 서버가 구독 클라이언트에 데이터를 푸시할 때마다 해당 데이터는 쿼리와 마찬가지로 실행된 구독의 구조를 따라야 한다.

```graphql
{
  "data": {
    "commentAdded": {
      "id": "123",
      "content": "What a thoughtful and well written post!"
    }
  }
}
```

## 전송 설정

구독은 일반적으로 지속적인 연결을 유지하기 때문에 Apollo 클라이언트가 쿼리 및 변형에 사용하는 기본 HTTP 전송을 사용하면 안 된다. `graphql-ws` 대신 Apollo 클라이언트 구독은 라이브러리를 통해 WebSocket을 통해 가장 일반적으로 통신한다.