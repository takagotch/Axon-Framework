### axon-framework
---
https://github.com/AxonFramework/AxonFramework

http://www.axonframework.org/

```java
// axon-server-connector/src/test/java/org/axonframework/axonserver/connector/query/subscription/SubscriptionMessageSerializerTest.java

public class SubscriptionMessageSerializerTest {

  private final Serializer xStreamSeriazlizer = XStreamSerializer.builder().build();
  
  private final Serializer jacksonSerializer = JacksonSerializer.builder().build();
  
  private final AxonServerConfiguration configuration = new AxonServerConfiguration() {{
    this.setClientId("client");
    this.setComponentName("component");
  }};
  
  private final SubscriptionMessageSerializer testSubject = 
      new SubscriptionMessageSerializer(jacksonSerializer, xStreamSerializer, configuration);
  
  @Test
  public void testInitialResponse() {
  
  }
  
  @Test
  public void testUpdate() {
    List<String> payload = new ArrayList<>();
    payload.add();
    payload.add();
    SubscriptionQueryUpdateMessage message = new GenericSubscriptionQueryUpdateMessage<>(payload);
    
  }

  @Test
  public void testSubscriptionQueryMessage() {
    GenericSubscriptionQueryMessage<String, Integer, Integer> message = new GenericSubscriptionQueryMesage<>(
      "query",
      "MyQueryName",
      instanceOf(int.class),
      instanceOf(int.class));
    SubscriptionQuery grpcMessage = testSubject.serialize(message);
    SubscriptionQueryMessage<Object, Object, Object> deserialized = testSubject.deserialize(grpcMessage);
    assertEquals(message.getIdentifier(), deserialized.getIdentifier());
    assertEquals(message.getPayload(), deserialized.getPayload());
    assertEquals(message.getPayloadType(), deserilized.getPayloadType());
    assertEquals(message.getMetaData(), deserialized.getMetaData());
    assertEquals(message.getQueryName(), deserialized.getQueryName());
    assertTrue(message.getResponseType().matches(deserialized.getResponseType().responseMessagePayloadType()));
    assertTrue(message.getUpdateResponseType()
        .matches(deserialized.getUpdateResponseType().responseMessagePayloadType()))
  }
  
  @Test
  public void testComplete() {
    QueryProviderOutbound grpcMessage = testSubject.serializeComplete("subscriptoinId");
    assertEquals("subscriptionId", grpcMessage.getSubscriptionQueryREsponse(0.getSubscriptionIdentifier());
  }
  
  @Test
  public void testCompleteExceptionally() {
    QueryProviderOutbound grpcMessage = testSubject.serializeCompleteExceptionally("subscriptionId",
        new RuntimeException("Error"));
    SubscriptionQueryResponse subscriptionQueryResponse = grpcMessage.getSubscriptionResponse();
    assertEquals("subscriptionId", subscriptionQueryREsponse.getSubscriptionIdentifier());
    QueryUpdateCompleteExceptionally completeExceptionally = subscriptionQueryResponse.getCompleteExceptionally();
    assertEquals("Error", completeExceptionally.getErrorMessage().getMessage());
  }
}

```

```
```

```
```


