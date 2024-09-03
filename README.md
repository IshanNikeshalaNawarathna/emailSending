# My Java EE 7 Application

## Overview
This is a Java EE 7 application developed to demonstrate enterprise-level features using the Glassfish server. The project utilizes JDK 8 for the development and deployment of enterprise components.

## Features
- **Java Persistence API (JPA):** Manages database interactions using JPA with Hibernate as the provider.
- **JavaServer Faces (JSF):** Provides a user interface using JSF.
- **RESTful Web Services:** Exposes services using JAX-RS.
- **Multithreading:** Utilizes Java threads for concurrent processing.

## Technologies Used
- **Java EE 7**
- **Glassfish Server**
- **JDK 8**

## Prerequisites
- **JDK 8**: Ensure JDK 8 is installed and configured on your system.
- **Glassfish Server**: Download and install Glassfish Server.

## Setup Instructions

1. **Clone the repository:**
   ```bash
   https://github.com/IshanNikeshalaNawarathna/email_sending
   ```
## Library class
   ```bash
package model;

import java.util.Properties;
import javax.mail.Message;
import javax.mail.MessagingException;
import javax.mail.PasswordAuthentication;
import javax.mail.Session;
import javax.mail.Transport;
import javax.mail.internet.InternetAddress;
import javax.mail.internet.MimeMessage;

public class Mail {

    private static final String APP_EMAIL = "user@gmail.com";
    private static final String APP_PASSWORD = "genarate your app password ";

    public static void sendMail(String email, String subject, String content) {

        Properties props = new Properties();
        props.put("mail.smtp.auth", "true");
        props.put("mail.smtp.starttls.enable", "true");
        props.put("mail.smtp.ssl.protocols", "TLSv1.2");
        props.put("mail.smtp.host", "smtp.gmail.com");
        props.put("mail.smtp.port", "587");

        Session session = Session.getInstance(props,
                new javax.mail.Authenticator() {
            protected PasswordAuthentication getPasswordAuthentication() {
                return new PasswordAuthentication(Mail.APP_EMAIL, Mail.APP_PASSWORD);
            }
        });

        try {
            Message message = new MimeMessage(session);
            message.setFrom(new InternetAddress(Mail.APP_EMAIL));
            message.setRecipients(Message.RecipientType.TO, InternetAddress.parse(email));
            message.setSubject(subject);
            message.setText(content);

            Transport.send(message);
            System.out.println("Email sent successfully!");

        } catch (MessagingException e) {
            throw new RuntimeException(e);
        }
    }
}

   ```
   ## How Access the Servlet
   
   ```bash

package controller;

import java.io.IOException;
import java.io.PrintWriter;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import model.Mail;

@WebServlet(name = "EmailSend", urlPatterns = {"/EmailSend"})
public class EmailSend extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        Mail.sendMail("youremail@gmail.com", "Hello", "Thnak you join me");
    }

}


   ```
