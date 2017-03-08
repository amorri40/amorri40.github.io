---
layout: post
title: "Simple XML in Java"
description: ""
category:
tags: []
---
{% include JB/setup %}

For a new project I needed to parse a prewritten xml file and extract information, instead of going to the bother of setting up a c++ xml library I decided to try out Java's built in class library for xml parsing.

First you will need to include the standard xml packages that we will use for simple xml loading:
```java
import javax.xml.parsers.*;
import org.w3c.dom.*;
import java.io.*;
```

Next we want to open an xml document to read from:
```java
DocumentBuilderFactory docBuilderFactory = DocumentBuilderFactory.newInstance();
DocumentBuilder docBuilder = docBuilderFactory.newDocumentBuilder();
Document doc = docBuilder.parse(new File("filename.xml"));
doc.getDocumentElement().normalize();
```

Next you will probably want to get all elements with a certain tag name, you can do this like so:
NodeList packageList = doc.getElementsByTagName("package"); //get all package elements

Now simply loop over all the package elemetns it found:
```java
for (int i = 0; i < packageList.getLength(); i++) {...}
```

Inside each package are subnodes so I would like to loop over them too (inside the loop above):
Node resNode = packageList.item(i);
NodeList packageDetails = resNode.getChildNodes();
```for (int ii = 0; ii < packageDetails.getLength(); ii++) { ..}```

Now I would like to print out only the nodes called name inside the package, so first check if the current node in the loop is called name:
```if (detailNode.getNodeName().equals("name")) {...}```

Now that we know this is the name node lets print the contents of the <name>contents</name>:
```System.out.println("Name of package:"+detailNode.getTextContent());```

Very simple indeed, although this is a simple example its amazing the information you can use from xml files using this simple method!