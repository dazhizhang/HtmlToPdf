# HtmlToPdf
http://davidxiaozhi.iteye.com/blog/1535679

参考
http://www.voidcn.com/blog/bolg_hero/article/p-2715293.html

注释
实际测试中，字体部分有问题，注释掉以后可以使用。
另外对复杂table的支持不是很好。
不支持变列数的table。

<dependency>  
    <groupId>com.itextpdf</groupId>  
    <artifactId>itextpdf</artifactId>  
    <version>5.1.1</version>  
</dependency>  
<!-- <dependency> <groupId>org.xhtmlrenderer</groupId> <artifactId>xhtmlrenderer</artifactId>   
    <version>8.3-atlassian</version> </dependency> -->  
<dependency>  
    <groupId>org.xhtmlrenderer</groupId>  
    <artifactId>core-renderer</artifactId>  
    <version>R8</version>  
</dependency>  
<dependency>  
    <groupId>dom4j</groupId>  
    <artifactId>dom4j</artifactId>  
    <version>1.6.1</version>  
</dependency>  
<dependency>  
    <groupId>com.lowagie</groupId>  


<artifactId>itext</artifactId>  
    <version>2.0.8</version>  
</dependency>  


try {  
            String outputFile = "D:/pdf/demo.pdf";  
            OutputStream os = new FileOutputStream(outputFile);  
            ITextRenderer renderer = new ITextRenderer();  
            // 解决中文支持问题  
            ITextFontResolver fontResolver = renderer.getFontResolver();  
            // simsun.ttc为字体文件  
            fontResolver.addFont("D:/pdf/simsun.ttc", BaseFont.IDENTITY_H,  
                    BaseFont.NOT_EMBEDDED);  
            //无论是方法1还是方法二对html格式要求都很严格  
              
            //=====1============直接拼接html代码 开始=====================  
              
            /*StringBuffer html = new StringBuffer(); 
            // DOCTYPE 必需写否则类似于 这样的字符解析会出现错误 
            html.append("<!DOCTYPE html PUBLIC \"-//W3C//DTD XHTML 1.0 Transitional//EN\" \"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd\">"); 
            html.append("<html xmlns=\"http://www.w3.org/1999/xhtml\">") 
                    .append("<head>") 
                    .append("<meta http-equiv=\"Content-Type\" content=\"text/html; charset=UTF-8\" />") 
                    .append("<style type=\"text/css\" mce_bogus=\"1\">body {font-family: SimSun;}</style>") 
                    .append("</head>").append("<body>") 
                    .append("<div>人员名单:</div>") 
                    .append("<table width=\"200\" border=\"1\">") 
                    .append("<tr>").append("<td>姓名:</td>") 
                    .append("<td>年龄:</td>").append("</tr>").append("<tr>") 
                    .append("<td>张小三</td>").append("<td>25</td>") 
                    .append("</tr>").append("</table>"); 
            html.append("</body></html>"); 
        renderer.setDocumentFromString(html.toString());*/  
              
            //=================直接拼接html代码 结束====================  
              
            //=====2======直接加载模版 start  
            renderer.setDocument(new File("D:/pdf/t.htm"));  
            //=====2======直接加载模版 end  
            // 解决图片的相对路径问题，如果是绝对路劲的话这个设置无用  
            renderer.getSharedContext().setBaseURL("http://www.baidu.com/img/");  
            renderer.layout();  
            renderer.createPDF(os);  
            os.close();  
  
        } catch (Exception e) {  
            // TODO: handle exception  
            e.printStackTrace();  
        }  
