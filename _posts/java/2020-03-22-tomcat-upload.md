---
layout: post
title: tomcat 上传大文件问题
category: java
tags: [tomcat]
description: tomcat 上传大文件问题
---


上传大文件时碰到这个错误
```

05-Apr-2020 23:00:20.435 SEVERE [http-nio-443-exec-90] org.apache.catalina.core.StandardWrapperValve.invoke Servlet.service() 
for servlet [action] in context with path [/gbc2] threw exception [org.apache.commons.fileupload.FileUploadException: Processing of multipart/form-data request failed. null] with root cause
org.apache.commons.fileupload.FileUploadException: Processing of multipart/form-data request failed. null
at org.apache.commons.fileupload.FileUploadBase.parseRequest(FileUploadBase.java:384)
at org.apache.commons.fileupload.servlet.ServletFileUpload.parseRequest(ServletFileUpload.java:116)
at guidebycell.action.mobi.UploadAction.upload3(UploadAction.java:127)
at sun.reflect.GeneratedMethodAccessor289.invoke(Unknown Source)
at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
at java.lang.reflect.Method.invoke(Method.java:498)
at org.apache.struts.actions.DispatchAction.dispatchMethod(DispatchAction.java:274)
at org.apache.struts.actions.DispatchAction.execute(DispatchAction.java:194)
at org.apache.struts.action.RequestProcessor.processActionPerform(RequestProcessor.java:419)
at org.apache.struts.action.RequestProcessor.process(RequestProcessor.java:224)
at org.apache.struts.action.ActionServlet.process(ActionServlet.java:1194)
at org.apache.struts.action.ActionServlet.doPost(ActionServlet.java:432)
at javax.servlet.http.HttpServlet.service(HttpServlet.java:648)
at javax.servlet.http.HttpServlet.service(HttpServlet.java:729)
at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:292)
at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:207)
at org.apache.tomcat.websocket.server.WsFilter.doFilter(WsFilter.java:52)
at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:240)
at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:207)
at guidebycell.filter.SessionFilter.doFilter(SessionFilter.java:63)
at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:240)
at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:207)
at guidebycell.filter.CharsetFilter.doFilter(CharsetFilter.java:33)
at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:240)
at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:207)
at org.apache.catalina.core.StandardWrapperValve.invoke(StandardWrapperValve.java:213)
at org.apache.catalina.core.StandardContextValve.invoke(StandardContextValve.java:106)
at org.apache.catalina.authenticator.AuthenticatorBase.invoke(AuthenticatorBase.java:606)
at org.apache.catalina.core.StandardHostValve.invoke(StandardHostValve.java:141)
at psiprobe.Tomcat80AgentValve.invoke(Tomcat80AgentValve.java:40)
at org.apache.catalina.valves.ErrorReportValve.invoke(ErrorReportValve.java:79)
at org.apache.catalina.valves.AbstractAccessLogValve.invoke(AbstractAccessLogValve.java:616)
at org.apache.catalina.core.StandardEngineValve.invoke(StandardEngineValve.java:88)
at org.apache.catalina.ha.tcp.ReplicationValve.invoke(ReplicationValve.java:318)
at org.apache.catalina.connector.CoyoteAdapter.service(CoyoteAdapter.java:522)
at org.apache.coyote.http11.AbstractHttp11Processor.process(AbstractHttp11Processor.java:1095)
at org.apache.coyote.AbstractProtocol$AbstractConnectionHandler.process(AbstractProtocol.java:672)
at org.apache.tomcat.util.net.NioEndpoint$SocketProcessor.doRun(NioEndpoint.java:1520)
at org.apache.tomcat.util.net.NioEndpoint$SocketProcessor.run(NioEndpoint.java:1476)
at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
at org.apache.tomcat.util.threads.TaskThread$WrappingRunnable.run(TaskThread.java:61)
at java.lang.Thread.run(Thread.java:748)
```

解决办法

```html 
<Connector port="8080" protocol="HTTP/1.1" URIEncoding="UTF-8" maxPostSize="-1"
       connectionUploadTimeout="36000000" disableUploadTimeout="false"
       connectionTimeout="60000" redirectPort="8443" />
 
```

参考 https://stackoverflow.com/questions/12476604/processing-of-multipart-form-data-request-failed-read-timed-out 

https://blog.csdn.net/n_meng/article/details/77306318


https://www.cnblogs.com/qingxinblog/p/3437169.html