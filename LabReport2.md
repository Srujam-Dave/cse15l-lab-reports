# Lab Report 2
### Part 1
- Code for ChatServer:
```
import java.io.IOException;
import java.net.URI;

class ChatHandler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    String message = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return message;
        } else if (url.getPath().equals("/add-message")) {
            String[] query = url.getQuery().split("&");
            String[] messageParameters;
            String[] userNameParameters;
            if (query.length == 2) {
                messageParameters = query[0].split("=");
                userNameParameters = query[1].split("=");
                if (messageParameters[0].equals("s") && userNameParameters[0].equals("user")) {
                    message += userNameParameters[1] + ": " + messageParameters[1] + "\n";
                    return message;
                }
            }
        }
        return "404 Not Found!";
    }
}

class ChatServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new ChatHandler());
    }
}
```
- Screenshot 1:
![Screenshot 1](./lab2sc1)

In order to launch the server, the code runs the main method in ChatServer, which takes in one argument - this is the port that the server runs on. Inside the main method, the static method start
(which is defined inside of the Server class) is called, which takes in a ChatHandler object as an argument, as well as the port number. The ChatHandler class contains a String field called message,
which contains the text that will be displayed to the user, and a method called handleRequest. handleRequest takes in the URI in the browser's address bar as an argument, and contains the variables 
query, messageParameters, and userNameParameters, all of are String arrays. They are all used to help process the query in the URI and format the text that will be added to message - the elements in 
query contain the entire query in the URL, the elements in userNameParameters contain the part of the query containing the username of the person sending the message, and the elements in 
messageParameters contain the parts used to process the message.

In this case, the URL path is /add-message, and the query is "?s=world&user=hello", which leads to the text "hello: world" being added to message and displayed to the user.

- Screenshot 2: 
![Screenshot 2](./lab2sc2)
The majority of the program is the same after the second URL was called - the main method is still running, and the start method has still launched the server using the same port number and
ChatHandler object. However, the URL has changed, with the query now being "?s=bar&user=foo". This changes the elements in query, messageParameters, and userNameParameters, and leads to the text
"foo: bar" being added to the message field and the text that is displayed to the user.

### Part 2
