## Westery的技术博客

Api接口交互标准<br/>
1.接口基于RESTful规范<br/>
2.接口返回统一采用json格式<br/>
3.由于部分浏览器对RESTful操作put delete会采取降级处理，所以对于更新和delete操作统一采取添加POST请求，并且添加_method:'put'/'delete'请求参数。<br/>
4.返回基于状态码对结果进行处理<br/>

HTTP状态码
200 OK - [GET]：服务器成功返回用户请求的数据，该操作是幂等的（Idempotent）。<br/>
201 CREATED - [POST/PUT/PATCH]：用户新建或修改数据成功。<br/>
202 Accepted - [*]：表示一个请求已经进入后台排队（异步任务）<br/>
204 NO CONTENT - [DELETE]：用户删除数据成功。<br/>
400 INVALID REQUEST - [POST/PUT/PATCH]：用户发出的请求有错误，服务器没有进行新建或修改数据的操作，该操作是幂等的。<br/>
401 Unauthorized - [*]：表示用户没有权限（令牌、用户名、密码错误）。<br/>
403 Forbidden - [*] 表示用户得到授权（与401错误相对），但是访问是被禁止的。<br/>
404 NOT FOUND - [*]：用户发出的请求针对的是不存在的记录，服务器没有进行操作，该操作是幂等的。<br/>
406 Not Acceptable - [GET]：用户请求的格式不可得（比如用户请求JSON格式，但是只有XML格式）。<br/>
410 Gone -[GET]：用户请求的资源被永久删除，且不会再得到的。<br/>
422 Unprocesable entity - [POST/PUT/PATCH] 当创建一个对象时，发生一个验证错误。<br/>
500 INTERNAL SERVER ERROR - [*]：服务器发生错误，用户将无法判断发出的请求是否成功。<br/>

5.返回的Json采用下面格式
<code>
[
  code:422000,
  status_code:422,
  message:'结果提示信息',
  data:[], 
  meta:[],
  errors:[]
]
  </code>

