
- [cxf验证](#cxf验证)


# cxf验证

- 客户端在soap中添加header信息，设置拦截器，将信息放在header中

    java代码：
    ```
        import org.apache.cxf.binding.soap.SoapHeader;
        import org.apache.cxf.binding.soap.SoapMessage;
        import org.apache.cxf.binding.soap.interceptor.AbstractSoapInterceptor;
        import org.apache.cxf.headers.Header;
        import org.apache.cxf.helpers.DOMUtils;
        import org.apache.cxf.interceptor.Fault;
        import org.apache.cxf.phase.Phase;
        import org.w3c.dom.Document;
        import org.w3c.dom.Element;

        import javax.xml.namespace.QName;
        import java.util.List;

        /**
         *
         */
        public class ClientAuthenticationHandler extends AbstractSoapInterceptor {

            public ClientAuthenticationHandler() {
                super(Phase.WRITE);
            }

            @Override
            public void handleMessage(SoapMessage message) throws Fault {
                QName qName = new QName("http://yourdomain.com/");
                Document doc = DOMUtils.createDocument();
                Element root = doc.createElement("AuthenticationToken");

                //添加用户校验信息
                Element username = doc.createElement("Username");
                username.setTextContent("cc-admin");

                Element password = doc.createElement("Password");
                password.setTextContent("asd1234");
                //可添加其他信息

                root.appendChild(username);
                root.appendChild(password);
                SoapHeader header = new SoapHeader(qName, root);
                // 获取SOAP消息的全部头
                List<Header> headers = message.getHeaders();
                headers.add(header);
            }

        }
    ```

    xml部分：
    ```
        <jaxws:client
            id=""
            serviceClass=""
            address="http://localhost:8080/gxfda_sys/syswebservice/ISysWebservice"
        >
        <jaxws:outInterceptors>
            <!--发送时的拦截器-->
            <ref bean="clientAuthenticationHandler" />
        </jaxws:outInterceptors>
        </jaxws:client>
    ```