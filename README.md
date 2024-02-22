# Interprocess communication & Networking in java

## 1- Client server:

**→ Client/Server Programming**:  model of interaction in a networked system where 'clients' request services and 'servers' provide them. This model has become prevalent in software development in recent years due to its efficiency and the way it facilitates distributed computing.

**→ Server = Services ≠ Host Machine**: This line is explaining the difference between a server, the services it provides, and the host machine.

- A 'server' in this context is a program or a computing device that provides services to other programs or devices, known as 'clients'.
- 'Services' are the specific functions or data that servers offer, such as serving web pages or handling FTP (File Transfer Protocol) requests.
- The 'host machine' is the physical or virtual machine on which the server program runs. This distinction is important because a single host machine can run multiple server programs, each providing different services.

→ E**xamples :** web pages and FTP to illustrate the types of services servers might offer. Web servers host and serve web pages to clients (like browsers), while FTP servers manage the transfer of files between clients and servers.

→ **Client and Server Locations**: The last point states that in a real-world application, the client and its corresponding server normally run on different machines. This is a typical setup where a user's device (running the client software) communicates over a network to a server located in a data center or cloud environment.

## 2- Peer 2 Peer

→  In some applications, such as messaging services, it is possible for programs on users’ machines to communicate directly with each other in what is called *peer-to peer* (or *P2P*) mode.

## 3- Ports and sockets:

→ ports and sockets are the entities lie at the heart of network communications.

- A port is a *logical* connection to a computer (as opposed to a physical connection) and is identified by a number in the range 1-65535.
- Port numbers in the range 1-1023 are normally set aside for the use of specified standard services. For example, port 80 is normally used by Web servers. each port supplying a service
- Application programs using port numbers 1024-65535

## 4- Internet services, URLs and DNS
![Untitled](https://github.com/mohammad-fahs/distributed-system-course/assets/109221274/75a6e718-cf9b-453a-9e55-413c463ec0b1)



## 5- TCP, IP, UDP & sockets

→ IP and TCP are the two commonest protocols used on the Internet and are almost invariably coupled together as TCP/IP. TCP is the higher level protocol that uses the lower level IP.

→ UDP is an unreliable protocol, since:

- it doesn't guarantee that each packet will  arrive;
- it doesn't guarantee that packets will be in the right order.

→ Different processes (programs) can communicate with each other across networks by means of sockets.

→ Java implements both **TCP/IP** sockets and **datagram** sockets (UDP sockets)

## 6- Middleware layers:

![Untitled 1](https://github.com/mohammad-fahs/distributed-system-course/assets/109221274/b1b27d81-5053-4842-a219-352192142eeb)


→ The middleware layer in the context of interprocess communication (IPC) serves as an abstraction layer between network applications and the lower-level networking protocols such as UDP (User Datagram Protocol) and TCP (Transmission Control Protocol). Here’s what each layer represents in the diagram you've provided:

1. **UDP and TCP**: These are transport layer protocols responsible for delivering data from one process to another. TCP provides reliable, connection-oriented communication, ensuring that data arrives in order and without errors. UDP provides a connectionless dispatch that does not guarantee delivery, order, or error checking, which can be useful for applications that require speed over reliability.
2. **Underlying interprocess communication primitives**: This layer includes the actual mechanisms and tools used for IPC such as sockets and message passing systems. Sockets are endpoints for sending and receiving data across a network. Message passing allows processes to communicate and synchronize their actions by sending messages to each other. This layer may also support multicast communication (sending a message to multiple recipients) and overlay networks (networks that are built on top of another network).
3. **Remote invocation, indirect communication**: This middleware layer provides higher-level abstractions for IPC, such as the ability for a process to invoke operations in a remote process (remote procedure calls or remote method invocation). Indirect communication might involve more complex patterns such as publish/subscribe or message queues, where the sender and receiver of a message do not need to interact with each other directly.
4. **Applications, services**: The top layer represents the end-user applications and services that make use of the underlying IPC mechanisms. These could be web applications, distributed databases, cloud services, etc., which rely on the middleware to manage the intricacies of IPC on their behalf.

The middleware layer facilitates communication between applications and services distributed across different systems and networks. It abstracts the complexities of the underlying network protocols and IPC primitives, providing developers with simpler interfaces to build distributed systems. Middleware can handle details such as connection management, scaling, reliability, and fault tolerance, allowing developers to focus on the application logic rather than the networking details.

## 7- Socket and Ports:

![Untitled 2](https://github.com/mohammad-fahs/distributed-system-course/assets/109221274/44596c05-18c3-42ff-b236-0d7cb18fc629)


**Sockets:**
A socket is an endpoint for sending and receiving data across a computer network. It is a combination of an IP address and a port number. Essentially, it provides a way for a program to specify the specific process it wishes to communicate with, both on the local machine and over the network.

There are different types of sockets that support various communication paradigms. For example:

- **Stream sockets** use TCP for communication, ensuring a reliable, ordered, and error-checked stream of bytes. These are used when you need to be sure that all data arrives intact and in order.
- **Datagram sockets** use UDP and are used for connectionless communication that may not guarantee delivery.

Sockets are created using system-level programming interfaces, such as the BSD socket API, which is available in most operating systems and provides functions for creating sockets, sending and receiving data, and closing connections.

**Ports:**
A port is a numerical identifier in network communications used to distinguish different processes on a single machine, ensuring that data traffic sent to a specific IP address can be routed to the correct application or service. Ports allow a single host with a single IP address to run network services. Each service that listens on a port can be uniquely identified by that port number.

Ports are divided into three ranges:

- **Well-known ports** range from 0 to 1023 and are assigned to common services by the Internet Assigned Numbers Authority (IANA). For example, HTTP uses port 80 and HTTPS uses port 443.
- **Registered ports** range from 1024 to 49151 and are not as tightly controlled but are still registered for certain services.
- **Dynamic or private ports** range from 49152 to 65535 and can be used by any application for temporary connections.

When a program on your computer reaches out to a server on the Internet, it uses a socket that combines the server's IP address and the port number of the service the program wants to use. The server listens for incoming requests on that port number and responds through the same channel.

The process is like calling a phone with multiple lines: the IP address is like the phone number, and the port number is like the specific extension you dial to speak to a particular department or person.

## 8- Java networking package (java.net)

→ Core package *java.net* contains a number of very useful classes that allow programmers to carry out network programming very easily.

### `InetAddress` Class

→ *`InetAddress`* handles Internet addresses both as host names and as IP addresses. Static method *`getByName`* of this class uses DNS (Domain Name System) to return the Internet address of a specified host name as an *`InetAddress`* object.

```java
public static void main(String[] args) {
        String host;
        Scanner input = new Scanner(System.in);
        System.out.println("enter host name");
        host = input.nextLine();
        try{ 
						//the current machine 
            System.out.println("The localhost is: "+ InetAddress.getLocalHost());

						//Address of the provided (google.com for example)
						InetAddress inetAddress =  InetAddress.getByName(host);
            System.out.println("IP Address: "+inetAddress.getHostAddress());
        }catch(UnknownHostException e) {
            System.out.println("Cant find IP Address for host "+host);
        }
    }
```

### TCP Socket

TCP/IP sockets is a **connection-orientated** link.  

⇒ Setting up a server process requires five steps:

- ***Create a `ServerSocket` object:*** The *`ServerSocket`* constructor requires a port number (1024-65535, for non-reserved ones) as an argument
    
    ```java
    ServerSocket servSock = new ServerSocket(1234);
    ```
    
- ***Put the server into a waiting state:*** The server waits indefinitely ('blocks') for a client to connect. It does this by calling method *accept* of class *`ServerSocket`*, which returns a *Socket* object when a connection is made.
    
    ```java
    Socket link = servSock.accept();
    ```
    
- ***Set up input and output streams:***  Methods *`getInputStream`* and *`getOutputStream`* of class *Socket* are used to get references to streams associated with the socket returned in step 2
    
    ```java
    DataInputStream in = new DataInputStream(clientSocket.getInputStream());
    DataOutputStream out = new DataOutputStream(clientSocket.getOutputStream());
    ```
    
    Remark: we can use `PrintWriter`: When you create a **`PrintWriter`** with a second argument of **`true`**, it will automatically flush the output buffer each time **`println()`** is called. Flushing the buffer means sending any buffered data to the client immediately without waiting for the buffer to fill up.
    
    ```java
    PrintWriter output = new PrintWriter(link.getOutputStream(), true);
    ```
    
- ***Send and receive data:***  Having set up our *Scanner* and *`PrintWriter`* objects, sending and receiving data is very straightforward. We simply use method *`nextLine`* for receiving data and method *`println`* for sending data
    
    ```java
    out.println("Awaiting data...");
    String message = in.nextLine();
    ```
    
- ***Close the connection:*** This is achieved via method *close* of class
    
    ```java
    link.close();
    ```
    

⇒ Setting up the corresponding client involves four steps

- ***Establish a connection to the server:*** We create a *Socket* object, supplying its constructor with the following two arguments:
    - the server's IP address (of type *`InetAddress`*);
    - the appropriate port number for the service.
- ***Set up input and output streams:*** These are set up in exactly the same way as the server streams were set up (by calling methods *`getInputStream`* and *`getOutputStream`* of the *Socket* object that was created in step 2).
- ***Send and receive data:*** The *Scanner* object at the client end will receive messages sent by the *`PrintWriter`* object at the server end, while the *`PrintWriter`* object at the client end will send messages that are received by the *Scanner* object at the server end (using methods *`nextLine`* and *`println`* respectively).
- ***Close the connection:*** This is exactly the same as for the server process (using method *close* of class *Socket*)

## 9- TCP Client / Server

→ write code of TCP Client server that sends a request and server replies 

### client code

1- create a socket object that needs a host and a port 

```java
InetAddress host = InetAddress.getLocalHost();
int serverPort = 7896;
Socket socket = new Socket(host,serverPort);        
```

2- Specify data input output streams 

```java
DataInputStream in = new DataInputStream(socket.getInputStream());
DataOutputStream out = new DataOutputStream(socket.getOutputStream());
```

3- send the message 

```java
String message = "this is Client message";
out.writeUTF(message);
```

4- get the reply from the server 

```java
String reply = in.readUTF();
System.out.println("Server reply: "+reply);
```

Over All code 

```java
public class TCPClient {
    public static void main(String[] args) {
        Socket socket = null;
        try{
            int serverPort = 7896;
            InetAddress host = InetAddress.getLocalHost();
            socket = new Socket(host,serverPort);

            DataInputStream in = new DataInputStream(socket.getInputStream());
            DataOutputStream out = new DataOutputStream(socket.getOutputStream());

            String message = "this is Client message";
            out.writeUTF(message);

            String reply = in.readUTF();
            System.out.println("Server reply: "+reply);

        }catch (UnknownHostException e){
            System.out.println("Sock:"+e.getMessage());
        }catch (EOFException e){
            System.out.println("EOF:"+e.getMessage());
        }catch (IOException e){
            System.out.println("IO:"+e.getMessage());
        }finally {
            if(socket !=null) try {
                socket.close();
            }catch (IOException e){
                System.out.println("close:"+e.getMessage());
            }
        }
    }
}
```

### Server code

1- create server socket

```java
int serverPort = 7896;
ServerSocket listenSocket = new ServerSocket(serverPort);
```

2- get the client socket

```java
Socket clientSocket = listenSocket.accept();
```

3- specify the input outputs 

```java
DataInputStream in = new DataInputStream(clientSocket.getInputStream());
DataOutputStream out = new DataOutputStream(clientSocket.getOutputStream());
```

4- retrieve the client message 

```java
String data = in.readUTF();
System.out.println("Client message: "+data);
```

5- send the response

```java
String response = "this is the server response";
out.writeUTF(response);
```

The overall code 

```java
public class TCPServer {
    public static void main(String[] args) {
        Socket clientSocket = null;
        try{
            int serverPort = 7896;
            ServerSocket listenSocket = new ServerSocket(serverPort);
            while(true) {
                clientSocket = listenSocket.accept();
                DataInputStream in = new DataInputStream(clientSocket.getInputStream());
                DataOutputStream out = new DataOutputStream(clientSocket.getOutputStream());

                String data = in.readUTF();
                System.out.println("Client message: "+data);

                String response = "this is the server response";
                out.writeUTF(response);
            }
        }catch (EOFException e) {
            System.out.println("EOF:" + e.getMessage());
        } catch (IOException e) {
            System.out.println("IO:" + e.getMessage());
        } finally {
            try {
                clientSocket.close();
            } catch (IOException e) {
                System.out.println("close failed");
            }
        }
    }
}
```

![Untitled 3](https://github.com/mohammad-fahs/distributed-system-course/assets/109221274/52439fcb-95ad-409c-b474-2fed776bdad3)


## 10- UDP Sockets:

→ Unlike TCP/IP sockets, datagram sockets are **connectionless**. That is to say, the connection between client and server is **not** maintained throughout the duration of the dialogue. Instead, each datagram packet is sent as an isolated transmission whenever necessary. As noted in Chapter 1, datagram (UDP) sockets provide a faster means of transmitting data than TCP/IP sockets, but they are unreliable.

Since the connection is not maintained between transmissions, the server does not create an individual *Socket* object for each client, as it did in our TCP/IP example. A further difference from TCP/IP sockets is that, instead of a *`ServerSocket`* object, the server creates a *`DatagramSocket`* object, as does each client when it wants to send datagram(s) to the server.

⇒ server side UDP Sockets: This process involves the following nine steps

- ***Create a `DatagramSocket` object:***  Just as for the creation of a *`ServerSocket`* object, this means supplying the object's constructor with the port number
    
    ```java
    DatagramSocket datagramSocket =new DatagramSocket(1234);
    ```
    
- ***Create a buffer for incoming datagrams:** This is achieved by creating an array of bytes*
    
    ```java
    byte[] buffer = new byte[256];
    ```
    
- ***Create a `DatagramPacket` object for the incoming datagrams:***  The constructor for this object requires two arguments: the previously-created byte array;
    
    ```java
    DatagramPacket inPacket = new DatagramPacket(buffer, buffer.length);
    ```
    
- ***Accept an incoming datagram:***  This is effected via the *receive* method of our *`DatagramSocket`* object, using our *`DatagramPacket`* object as the receptacle
    
    ```java
    datagramSocket.receive(inPacket);
    ```
    
- ***Accept the sender's address and port from the packet:*** Methods *`getAddress`* and *`getPort`* of our *`DatagramPacket`* object are used for this.
    
    ```java
    InetAddress clientAddress = inPacket.getAddress();
    int clientPort = inPacket.getPort();
    ```
    
- ***Retrieve the data from the buffer:***  For convenience of handling, the data will be retrieved as a string, using an overloaded form of the *String* constructor that takes three arguments:
    - a byte array;
    - the start position within the array (= 0 here);
    - the number of bytes (= full size of buffer here).
    
    ```java
    String message = new String(inPacket.getData(),0,inPacket.getLength());
    ```
    
- ***Create the response datagram:***  Create a *`DatagramPacket`* object, using an overloaded form of the constructor that takes four arguments:
    - the byte array containing the response message;
    - the size of the response;
    - the client's address;
    - the client's port number.
    
     The first of these arguments is returned by the *`getBytes`* method of the *`String*class` (acting on the desired *String* response).
    
    ```java
    DatagramPacket outPacket = new DatagramPacket(response.getBytes(), response.length(),clientAddress, clientPort);
    ```
    
- ***Send the response datagram:*** This is achieved by calling method *send* of our *`DatagramSocket`* object, supplying our outgoing *`DatagramPacket`* object as an argument.
    
    ```java
    datagramSocket.send(outPacket);
    ```
    
- ***Close the `DatagramSocket`:*** This is effected simply by calling method *close* of our *`DatagramSocket`* object
    
    ```java
    datagramSocket.close();
    ```
    

⇒ client side have 8 steps: 

- ***Create a `DatagramSocket` object:** This is similar to the creation of a `DatagramSocket` object in the server program, but with the important difference that the constructor here requires no argument, since a default port (at the client end) will be used.*
    
    ```java
    DatagramSocket datagramSocket = new DatagramSocket();
    ```
    
- ***Create the outgoing datagram***
    
    ```java
    DatagramPacket outPacket=newDatagramPacket(message.getBytes(), message.length(), host, PORT);
    ```
    
- ***Send the datagram message:***  Just as for the server, this is achieved by calling method *send* of the *`DatagramSocket`* object, supplying our outgoing *`DatagramPacket`* object as an argument.
    
    ```java
    datagramSocket.send(outPacket);
    ```
    
- ***Create a buffer for incoming datagrams***
    
    ```java
    byte[] buffer = new byte[256];
    ```
    
- ***Create a `DatagramPacket` object for the incoming datagrams***
    
    ```java
    DatagramPacket inPacket =new DatagramPacket(buffer,buffer.length);
    ```
    
- ***Accept an incoming datagram***
    
    ```java
    datagramSocket.receive(inPacket);
    ```
    
- ***Retrieve the data from the buffer***
    
    ```java
    String response =new String(inPacket.getData(),0, inPacket.getLength());
    ```
    
- ***Close the `DatagramSocket`:***
    
    ```java
    datagramSocket.close();
    ```
    

## 11- UDP Client / Server

→ Write code of UDP Client server that sends a request and server replies 

### client

1- create datagram pack request that needs the Host, port and contains the message as array of bytes in addition to the size of the array bytes 

```java
String message = "client message will be sent to server"
InetAddress Host = InetAddress.getLocalHost();
byte[] m = message.getBytes();
int serverPort = 6789;
DatagramPacket request = new DatagramPacket(m,  m.length, Host, serverPort);
```

2- create the socket and send the request 

```java
DatagramSocker socket = new DatagramSocket();
socker.send(request);
```

3- now the client will receive the reply from server using the socket he used to send the request and convert it to String 

```java
// Receive the reply 
byte[] buffer = new byte[1000];
DatagramPacket reply = new DatagramPacket(buffer, buffer.length);
socket.receive(reply);
//convert it into string
String reply = new String(reply.getData(),0,reply.getLength());
```

- Client Over all code
    
    ```java
    public class UDPClient {
        public static void main(String[] args) {
            DatagramSocket aSocket = null;
    
            try{
                InetAddress aHost = InetAddress.getLocalHost();
                byte[] m = "this is the client message".getBytes();
                int serverPort = 6789;
                DatagramPacket request = new DatagramPacket(m,  m.length, aHost, serverPort);
    
                aSocket = new DatagramSocket();
                aSocket.send(request);
    
                byte[] buffer = new byte[1000];
                DatagramPacket reply = new DatagramPacket(buffer, buffer.length);
                aSocket.receive(reply);
    
                System.out.println("Reply: " + new String(reply.getData(),0,reply.getLength()));
            }catch (SocketException e){
                System.out.println("Socket: " + e.getMessage());
            }catch (IOException e){
                System.out.println("IO: " + e.getMessage());
            }finally {
                if(aSocket != null) aSocket.close();
            }
        }
    }
    ```
    

### Server

1- create server datagram socket with the same port client uses to send the message 

```java
DatagramSocket severSocket = new DatagramSocket(6789)
```

2- enter a while infinite loop to keep waiting for any message and receiving it then send a reply 

```java
//save the request data in array of bytes 
byte[] buffer = new byte[1000];
//while loop to keep waiting for new requests 
while(true){
	//create request and receive it 
	DatagramPacket request = new DatagramPacket(buffer, buffer.length);
	sevrerSocket.receive(request);
	//convert the request data to String 
	String requestMessage = new String(request.getData(),0,request.getLength());
	//print message if needed
	System.out.println(requestMessage);
	//create and send reply 
	String messageOut = "reply message from server";
  DatagramPacket reply = new DatagramPacket(messageOut.getBytes(),messageOut.getBytes().length, request.getAddress(), request.getPort());
  serverSocket.send(reply);
	
}

```

- Over all code
    
    ```java
    public class UDPServer {
        public static void main(String[] args) {
            DatagramSocket aSocket = null;
    
            try {
                aSocket = new DatagramSocket(6789);
                byte[] buffer = new byte[1000];
                while (true) {
                    DatagramPacket request = new DatagramPacket(buffer, buffer.length);
                    aSocket.receive(request);
    
                    System.out.println("message in: "+ new String(request.getData(),0,request.getLength()));
    
                    String messageOut = "reply message from server";
                    DatagramPacket reply = new DatagramPacket(messageOut.getBytes(),messageOut.getBytes().length, request.getAddress(), request.getPort());
                    aSocket.send(reply);
                }
            } catch (SocketException e) {
                System.out.println("Socket: " + e.getMessage());
            } catch (IOException e) {
                System.out.println("IO: " + e.getMessage());
            } finally {
                if (aSocket != null) aSocket.close();
            }
        }
    }
    ```
    

## 12-Indication of JAVA serialized form

![Untitled 4](https://github.com/mohammad-fahs/distributed-system-course/assets/109221274/1787177d-4ce8-4871-8ba7-09fbe4dbfbaf)


Serialization is the process of converting an object into a byte stream, which can then be written to a file, sent over a network, or stored in a database. The byte stream can then be deserialized later to recreate the object from the byte stream.

Here's a breakdown of the slide's contents:

- The left column under "Serialized values" lists the components of a serialized object. The object is of class **`Person`**.
- The first row shows "8-byte version number," which likely represents the serialization version UID, a unique identifier that JVM uses to ensure that a loaded class corresponds exactly to a serialized object.
- The next rows list instance variables for the **`Person`** class with their types and values. There's an **`int`** named **`year`** with the value **`1984`**, a **`java.lang.String`** named **`name`** with the value **`Smith`**, and another **`java.lang.String`** named **`place`** with the value **`London`**.
- The right column under "Explanation" provides a brief description of what each entry in the serialized form represents, such as the class name, version number, and the names and values of instance variables.

The mention of **`h0`** and **`h1`** at the bottom of the slide indicates that these are handles, which are references used internally by the serialization mechanism to keep track of objects. This is done to maintain the identity and references of objects, for example, if multiple objects reference the same **`String`**, they will all point to the same handle, ensuring that the relationship is maintained when the object graph is deserialized.

The note at the bottom clarifies that the true serialized form also contains additional type markers, which are not shown in the simplified representation on the slide. These markers are metadata that the Java Virtual Machine (JVM) uses to reconstruct the objects during deserialization.

## 13- XML Definition of person structure with usage illustration

XML is a flexible way to create information formats and electronically share structured data via the internet, as well as via corporate networks. It is used in a wide variety of applications such as configuration files, communication protocols, web services, and for the storage and transfer of data between different systems.

### **XML Definition of the Person Structure**

below is a basic XML (eXtensible Markup Language) structure for a **`Person`**. XML is a markup language that defines a set of rules for encoding documents in a format that is both human-readable and machine-readable. The primary purpose of XML is to facilitate the sharing of structured data across different information systems, particularly via the internet.

- **`<person id="123456789">`** is the root element representing a **`Person`**. It has an attribute **`id`** with a value of **`123456789`**.
- Nested within the **`person`** element are child elements:
    - **`<name>Smith</name>`** represents the person's name.
    - **`<place>London</place>`** represents the place associated with the person.
    - **`<year>1984</year>`** represents the year, possibly the person's birth year.
- **`<!-- a comment -->`** is a comment in XML, which is ignored by the parser and can be used to include notes or explanations in the code.

```java

<person id="123456789">
		<name>Smith</name>
		<place>London</place>
		<year>1984</year>
		<!-- a comment -->
</person >
```

### **Illustration of the Use of a Namespace in the Person Structure**

the use of XML namespaces, which provide a method to avoid element name conflicts by qualifying names with a namespace identifier.

- The **`xmlns:pers`** attribute in the **`person`** element declares a namespace with the URI **`http://www.cdk5.net/person`**, which is a way to uniquely identify the elements and attributes used in this XML. This URI is not required to be a working link; it serves as a unique identifier.
- The **`pers:`** prefix is used before each element name (**`name`**, **`place`**, **`year`**) to associate them with the namespace declared earlier. This is especially useful when combining XML documents from different XML applications or when using custom tags that might conflict with standard tags.

```java
<person pers:id="123456789" xmlns:pers = "http://www.cdk5.net/person">
	<pers:name> Smith </pers:name>
	<pers:place> London </pers:place >
	<pers:year> 1984 </pers:year>
</person>
```

## 14- XML schema for the *Person* structure

a snippet of an XML Schema definition (XSD) for a **`Person`** structure. An XML Schema defines the structure and types of data that an XML document can contain. It serves as a blueprint for creating valid XML documents.

Here's an explanation of each part of the schema:

- **`<xsd:schema xmlns:xsd="URL of XML schema definitions">`**: This is the root element of the schema and it declares a namespace **`xsd`** that is associated with a URL (which should be provided where the placeholder **`URL of XML schema definitions`** is). This URL is the namespace that indicates the document is an XSD and it is typically **`http://www.w3.org/2001/XMLSchema`**.
- **`<xsd:element name="person" type="personType"/>`**: This line defines an element called **`person`** that is of the type **`personType`**. This **`personType`** is a complex type that will be defined further in the schema.
- **`<xsd:complexType name="personType">`**: A complex type named **`personType`** is being defined here. Complex types are used in XML Schemas to define elements that contain other elements or attributes.
- **`<xsd:sequence>`**: This element is used within complex types to define a sequence of elements that must appear in the XML document in the order they are listed.
    - **`<xsd:element name="name" type="xs:string"/>`**: Inside the **`sequence`**, it defines an element named **`name`** that will contain string data.
    - **`<xsd:element name="place" type="xs:string"/>`**: Similarly, an element named **`place`** is defined to hold a string value.
    - **`<xsd:element name="year" type="xs:positiveInteger"/>`**: An element named **`year`** is defined to hold a positive integer.
- **`</xsd:sequence>`**: This closes the sequence definition, indicating the end of the ordered list of elements within **`personType`**.
- **`<xsd:attribute name="id" type="xs:positiveInteger"/>`**: This defines an attribute for the complex type **`personType`**. The **`id`** attribute is expected to be a positive integer.
- **`</xsd:complexType>`**: This closes the **`complexType`** definition for **`personType`**.
- **`</xsd:schema>`**: Finally, this closes the schema definition.

The schema is a formal specification for what the **`Person`** XML document should contain: a **`person`** element with a sequence of child elements (**`name`**, **`place`**, **`year`**) and an **`id`** attribute. Each of these child elements and attributes has a specified data type, like **`string`** or **`positiveInteger`**. This ensures that any XML document matching this schema will have a consistent structure and data type, which is crucial for the data interchange between systems.

```java
<xsd:schema  xmlns:xsd = URL of XML schema definitions	 >
	<xsd:element name= "person" type ="personType" />
		<xsd:complexType name="personType">
			<xsd:sequence>
				<xsd:element name = "name"  type="xs:string"/> 
				<xsd:element name = "place"  type="xs:string"/> 
				<xsd:element name = "year"  type="xs:positiveInteger"/> 
			</xsd:sequence>
			<xsd:attribute name= "id"   type = "xs:positiveInteger"/>
		</xsd:complexType>
</xsd:schema>
```

## 15-Representation of a remote object reference

![Untitled 5](https://github.com/mohammad-fahs/distributed-system-course/assets/109221274/7a8279fa-f07d-48ce-9cf7-1df5f72dc6d9)


- **32 bits - Internet address**: This is likely an IPv4 address, which is 32 bits in length. It identifies the network location of the host where the remote object resides.
- **32 bits - Port number**: This specifies the port number on the host used for communication with the remote object. While port numbers are actually 16 bits long, this representation could be including additional information or simply aligning to 32 bits for consistency in the structure.
- **32 bits - Time**: This could represent a timestamp related to the remote object. The specifics of what 'time' means in this context aren't clear without additional information, but it could, for instance, be the time when the reference was created or the time when the object was last updated.
- **32 bits - Object number**: This is an identifier for the specific object within the remote system. It differentiates this object from other objects that might exist on the same host.
- **32 bits - Interface of remote object**: This might represent some form of identifier or descriptor for the interface that the remote object implements. An interface, in this context, would define the methods that can be called on the remote object.

This kind of structure would be used in systems that employ remote procedure calls (RPCs) or in systems that use object request brokers (like CORBA). It ensures that any call made to a remote object can be correctly routed to the right location and to the right instance of an object, with the correct interface for method invocation. The time element might be used for cache invalidation, synchronization, or versioning, but without more context, it's hard to say exactly what its purpose is.

## 16- Multicast peer joins a group and sends and receives datagrams

## 17- Summation Example UDP:

→ Client code 

```java
public class UDPClient {
    public static void main(String[] args) throws IOException {
        BufferedReader userIn = new BufferedReader(new InputStreamReader(System.in));
        DatagramSocket clientSocket = new DatagramSocket();
        InetAddress IPAddress = InetAddress.getLocalHost();

        byte[] sendData;
        byte[] receiveData = new byte[1024];

        try {
            System.out.print("Enter the first number: ");
            String num1 = userIn.readLine();
            System.out.print("Enter the second number: ");
            String num2 = userIn.readLine();

            String sentence = num1 + "," + num2;
            sendData = sentence.getBytes();

            // Send packet to server
            DatagramPacket sendPacket = new DatagramPacket(sendData, sendData.length, IPAddress, 9876); // Server port
            clientSocket.send(sendPacket);

            // Receive packet from server
            DatagramPacket receivePacket = new DatagramPacket(receiveData, receiveData.length);
            clientSocket.receive(receivePacket);
            String modifiedSentence = new String(receivePacket.getData(), 0, receivePacket.getLength());

            System.out.println("summation result is "+modifiedSentence);
        }catch (SocketException e){
            System.out.println("Socket: " + e.getMessage());
        }catch (IOException e){
            System.out.println("IO: " + e.getMessage());
        }finally {
            clientSocket.close();
        }
    }
}
```

→ Server code 

```java
public class UDPServer {
    public static void main(String[] args) {
        DatagramSocket socket = null;
        try {
            socket = new DatagramSocket(9876); // Server will listen on port 9876
            byte[] receiveData = new byte[1024];
            byte[] sendData;

            while (true) {
                // Receive packet
                DatagramPacket receivePacket = new DatagramPacket(receiveData, receiveData.length);
                socket.receive(receivePacket);
                String sentence = new String(receivePacket.getData(), 0, receivePacket.getLength());
                // Extract numbers and compute sum
                String[] numbers = sentence.split(",");
                int num1 = Integer.parseInt(numbers[0].trim());
                int num2 = Integer.parseInt(numbers[1].trim());
                int sum = num1 + num2;

                // Send response back to client
                sendData = Integer.toString(sum).getBytes();
                DatagramPacket sendPacket = new DatagramPacket(sendData, sendData.length, receivePacket.getAddress(), receivePacket.getPort());
                socket.send(sendPacket);
            }
        } catch (SocketException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (socket != null && !socket.isClosed()) {
                socket.close();
            }
        }
    }
}
```

### Output example
![Untitled 6](https://github.com/mohammad-fahs/distributed-system-course/assets/109221274/43aa15e6-829b-490e-8644-cc77c1aafa26)



## 18- Summation Example using TCP

→ Client Code 

```java
public class TCPClient {
    public static void main(String[] args) {
        BufferedReader userIn = new BufferedReader(new InputStreamReader(System.in));
        Socket socket = null;
        try{
            int serverPort = 7896;
            InetAddress host = InetAddress.getLocalHost();
            socket = new Socket(host,serverPort);

            DataInputStream in = new DataInputStream(socket.getInputStream());
            DataOutputStream out = new DataOutputStream(socket.getOutputStream());

            System.out.print("Enter the first number: ");
            String num1 = userIn.readLine();
            System.out.print("Enter the second number: ");
            String num2 = userIn.readLine();

            String sentence = num1 + "," + num2;
            out.writeUTF(sentence);

            String reply = in.readUTF();
            System.out.println("Server reply: "+reply);

        }catch (UnknownHostException e){
            System.out.println("Sock:"+e.getMessage());
        }catch (EOFException e){
            System.out.println("EOF:"+e.getMessage());
        }catch (IOException e){
            System.out.println("IO:"+e.getMessage());
        }finally {
            if(socket !=null) try {
                socket.close();
            }catch (IOException e){
                System.out.println("close:"+e.getMessage());
            }
        }
    }
}
```

→ Server Code 

```java
public class TCPServer {
    public static void main(String[] args) {
        Socket clientSocket = null;
        try{
            int serverPort = 7896;
            ServerSocket listenSocket = new ServerSocket(serverPort);
            while(true) {
                clientSocket = listenSocket.accept();
                DataInputStream in = new DataInputStream(clientSocket.getInputStream());
                DataOutputStream out = new DataOutputStream(clientSocket.getOutputStream());

                String data = in.readUTF();
                String[] numbers = data.split(",");
                int num1 = Integer.parseInt(numbers[0].trim());
                int num2 = Integer.parseInt(numbers[1].trim());
                int sum = num1 + num2;

                String response = "the summation of number is "+sum;
                out.writeUTF(response);
            }
        }catch (EOFException e) {
            System.out.println("EOF:" + e.getMessage());
        } catch (IOException e) {
            System.out.println("IO:" + e.getMessage());
        } finally {
            try {
                clientSocket.close();
            } catch (IOException e) {
                System.out.println("close failed");
            }
        }
    }
}
```

### Output example:
![Untitled 7](https://github.com/mohammad-fahs/distributed-system-course/assets/109221274/5b86fb77-445d-4553-b691-2729c3d9c4d6)

