官网地址：https://square.github.io/retrofit/

## **GET**

1. `http://192.168.43.173/api/trades`

```
//简单的get请求(没有参数)
 @GET("trades")
 Call<TradesBean> getItem();123
```

2. `http://192.168.43.173/api/trades/{userId}`

```
//简单的get请求(URL中带有参数)
  @GET("News/{userId}")
  Call<TradesBean> getItem(@Path("userId") String userId);123
```

```
//简单的get请求(URL中带有两个参数)
  @GET("News/{userId}")
  Call<TradesBean> getItem(@Path("userId") String userId,@Path("type") String type);123
```

3. `<http://192.168.43.173/api/trades?userId=>{用户id}`

```
//参数在url问号之后
 @GET("trades")
 Call<TradesBean> getItem(@Query("userId") String userId);
1234
```

4. `<http://192.168.43.173/api/trades?userId=>{用户id}&type={类型}`

```
 @GET("trades")
 Call<TradesBean> getItem(@QueryMap Map<String, String> map);12
```

```
 @GET("trades")
 Call<TradesBean> getItem(
                @Query("userId") String userId,
                @QueryMap Map<String, String> map);1234
```

## **POST**

1. `<http://192.168.43.173/api/trades/>{userId}`

```
//需要补全URL,post的数据只有一条reason
 @FormUrlEncoded
 @POST("trades/{userId}")
 Call<TradesBean> postResult(
         @Path("userId") String userId,
         @Field("reason") String reason;
```

2. `<http://192.168.43.173/api/trades/>{userId}?token={token}`

```
//需要补全URL,问号后需要加token,post的数据只有一条reason
 @FormUrlEncoded
 @POST("trades/{userId}")
 Call<TradesBean> postResult(
         @Path("userId") String userId,
         @Query("token") String token,
         @Field("reason") String reason;
```

```
//post一个对象
 @POST("trades/{userId}")
 Call<TradesBean> postResult(
         @Path("userId") String userId,
         @Query("token") String token,
         @Body TradesBean bean;
```

```
//用不同注解post一个实体
 @POST("trades/{userId}")
 Call<TradesBean> postResult(
         @Part("entity") TradesBean bean;1234
```

## **PUT**

```
//put一个实体
 @PUT("trade/carInfo/{pid}")
 Call<TradesBean> putInfo(
             @Path("pid") Int pid,
             @Body CarInfoBean carInfoBean;)12345
```

## **DELETE**

1. `<http://192.168.43.173/api/trades/>{userId}`

```
//补全url
 @DELETE("trades/{userId}")
 Call<TradesBean> deleteInfo(
         @Path("userId") String userId;  1234
```

2. `<http://192.168.43.173/api/trades/>{userId}?token={token}`

```
//补全url并且后面还token
 @DELETE("trades/{userId}")
 Call<TradesBean> deleteInfo(
         @Path("userId") String userId,
         @Query("token") String token;)  
```