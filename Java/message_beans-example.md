## Message Beans Example

#### TestMessageBean
```java
package edu.matc.enterprisejava.mdb;

import javax.annotation.Resource;
import javax.ejb.MessageDriven;
import javax.jms.*;
import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import org.apache.log4j.*;

@WebServlet(
        name = "testMessageBean",
        urlPatterns = { "/testMessageBean" }
)
@MessageDriven
public class TestMessageBean extends HttpServlet implements MessageListener {

    @Resource
    private ConnectionFactory connectionFactory;

    @Resource(name = "MessageBean")
    private Queue questionQueue;

    private final Logger logger = Logger.getLogger(this.getClass());

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        run(req.getParameter("color"));

        req.setAttribute("status", "Message sent, check the console/logs to " +
                "view the message");
        RequestDispatcher dispatcher = req.getRequestDispatcher("/index.jsp");
        dispatcher.forward(req, resp);
    }

    public void run(String message) {

        Session session = null;
        Connection connection = null;

        try {

            connection = connectionFactory.createConnection();

            connection.start();

            session = connection.createSession(false, Session.AUTO_ACKNOWLEDGE);

            final MessageProducer questions = session.createProducer(questionQueue);

            questions.send(session.createTextMessage(message));

        } catch (Exception exception) {
            logger.error(exception.getStackTrace());


        } finally {

            try {
                if (session != null) {
                    session.close();
                }
                if (connection != null) {
                    connection.close();
                }
            } catch (Exception exception) {
                logger.error(exception.getStackTrace());
            }
        }
    }

    public void onMessage(Message message) {
        TextMessage mess = (TextMessage) message;
        String m;
        try {
            m = mess.getText();
            logger.info("TestMessageBean: " + m);
        } catch (JMSException exception) {
            logger.error(exception.getStackTrace());
        }
    }

}
```

#### MessageBean
```java
package edu.matc.enterprisejava.mdb;

import org.apache.log4j.Logger;
import javax.annotation.Resource;
import javax.ejb.MessageDriven;
import javax.jms.*;

@MessageDriven
public class MessageBean implements MessageListener {

    private final Logger logger = Logger.getLogger(this.getClass());

    @Resource
    private ConnectionFactory connectionFactory;

    @Resource(name = "TestMessageBean")
    private Queue answerQueue;

    public MessageBean() {
    }

    public void onMessage(Message message) {
        TextMessage mess = (TextMessage) message;
        String m = "";
        try {
            m = mess.getText();
        } catch (JMSException exception) {
            logger.error(exception.getStackTrace());
        }
        String response = "";
        if (m.equals("blue")) {
            response = "You are calm, cool, and able to keep things more even keel than most.";
        }
        if (m.equals("red")) {
            response = "You are bold, sexually charged, and want to make a lasting impression.";
        }
        if (m.equals("green")) {
            response = "You are prone to putting lots of importance on money and security.";
        }
        if (m.equals("orange")) {
            response = "You are friendly, easy going, and probably a theater major.";
        }
        if (m.equals("purple")) {
            response = "You are a wee bit off, but in your own special way.";
        }
        if (m.equals("grey")) {
            response = "You are afraid of commitment.";
        }
        if (m.equals("pink")) {
            response = "You are a little naive, sheltered, and have delicate sensibilities.";
        }
        if (m.equals("black")) {
            response = "You are part moody, part sophisticated.";
        }
        if (m.equals("white")) {
            response = "You are innocent. Or at least you think you are.";
        }
        if (m.equals("brown")) {
            response = "You are simple and comfortable.";
        }
        if (m.equals("yellow")) {
            response = "You are a happy idealist who is underestimated far too often.";
        }

        Session session = null;
        Connection connection = null;

        try {

            connection = connectionFactory.createConnection();

            connection.start();

            session = connection.createSession(false, Session.AUTO_ACKNOWLEDGE);

            final MessageProducer questions = session.createProducer(answerQueue);

            questions.send(session.createTextMessage(response));

        } catch (Exception exception) {
            logger.error(exception.getStackTrace());


        } finally {

            try {
                if (session != null) {
                    session.close();
                }
                if (connection != null) {
                    connection.close();
                }
            } catch (Exception exception) {
                logger.error(exception.getStackTrace());
            }
        }
    }

}
```

#### Index file
```html
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ page isELIgnored="false" %>
<html>
<head>
  <title>MDB Exercise</title>
</head>
<body>
<h2>What is your favorite color?<h2>
  <form action="testMessageBean" method="get">
    <select name="color">
      <option value="blue">Blue</option>
      <option value="red">Red</option>
      <option value="green">Green</option>
      <option value="orange">Orange</option>
      <option value="purple">Purple</option>
      <option value="grey">Grey</option>
      <option value="pink">Pink</option>
      <option value="black">Black</option>
      <option value="white">Pink</option>
      <option value="brown">Brown</option>
      <option value="yellow">Yellow</option>
    </select>
    <button type="submit">Send</button>
  </form>
  <br />
  ${status}
</body>
</html>
```
