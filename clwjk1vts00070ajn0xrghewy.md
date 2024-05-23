---
title: "Integrating Payment Gateways in Flutter: Learn How to Add Payment Processing to Your Flutter App"
seoTitle: "Mastering Payment Gateway Integration in Flutter: Add Payment Processi"
seoDescription: "Discover how to seamlessly integrate payment gateways into your Flutter app. Learn step-by-step methods for adding secure payment processing and enhancing u"
datePublished: Thu May 23 2024 17:56:58 GMT+0000 (Coordinated Universal Time)
cuid: clwjk1vts00070ajn0xrghewy
slug: integrating-payment-gateways-in-flutter-learn-how-to-add-payment-processing-to-your-flutter-app
tags: mobileappdevelopment, flutter-development, flutter-widgets, flutternik, devsnik, paymentgatewayintegration, flutterplugins, mobilepayments, securetransactions, flutterlibraries, ravi-patel-flutter

---

## Introduction

In this tutorial, we'll learn how to integrate a payment gateway into a Flutter app. Payment gateways are crucial for any e-commerce app, subscription service, or any application that requires financial transactions. We’ll be using Stripe as our payment processor, given its ease of use and robust API.

## Prerequisites

Before we begin, ensure you have the following:

* Flutter installed on your machine
    
* A basic understanding of Flutter
    
* A Stripe account (you can sign up at [Stripe](https://stripe.com/))
    

## Setting Up Your Flutter Environment

1. **Create a new Flutter project:**
    
    ```bash
    flutter create payment_app
    cd payment_app
    ```
    
2. **Add dependencies:**
    
    Open `pubspec.yaml` and add the following dependencies:
    
    ```yaml
    dependencies:
      flutter:
        sdk: flutter
      http: ^0.14.0
      stripe_payment: ^1.0.9
    ```
    
    Run `flutter pub get` to install the new dependencies.
    

## Setting Up Stripe

1. **Install the Stripe CLI:** Follow the instructions on the [Stripe CLI installation page](https://stripe.com/docs/stripe-cli).
    
2. **Create a Stripe account and obtain API keys:**
    
    * Sign in to your Stripe dashboard.
        
    * Navigate to the Developers section and get your publishable and secret keys.
        
3. **Start a local server to handle payments:** For simplicity, we'll use a Node.js server to handle payments. Here’s a basic example:
    
    ```javascript
    // server.js
    const express = require('express');
    const stripe = require('stripe')('your_secret_key_here');
    const bodyParser = require('body-parser');
    const cors = require('cors');
    
    const app = express();
    app.use(bodyParser.json());
    app.use(cors());
    
    app.post('/create-payment-intent', async (req, res) => {
      const { amount } = req.body;
      const paymentIntent = await stripe.paymentIntents.create({
        amount,
        currency: 'usd',
      });
    
      res.send({
        clientSecret: paymentIntent.client_secret,
      });
    });
    
    app.listen(4242, () => console.log('Server running on port 4242'));
    ```
    
    Run your server:
    
    ```bash
    node server.js
    ```
    

## Building the Flutter UI

1. **Create the basic UI:**
    
    Open `lib/main.dart` and replace its content with the following code:
    
    ```dart
    import 'package:flutter/material.dart';
    import 'package:stripe_payment/stripe_payment.dart';
    import 'package:http/http.dart' as http;
    import 'dart:convert';
    
    void main() {
      runApp(MyApp());
    }
    
    class MyApp extends StatelessWidget {
      @override
      Widget build(BuildContext context) {
        return MaterialApp(
          home: PaymentScreen(),
        );
      }
    }
    
    class PaymentScreen extends StatefulWidget {
      @override
      _PaymentScreenState createState() => _PaymentScreenState();
    }
    
    class _PaymentScreenState extends State<PaymentScreen> {
      @override
      void initState() {
        super.initState();
        StripePayment.setOptions(
          StripeOptions(
            publishableKey: "your_publishable_key_here",
            merchantId: "Test",
            androidPayMode: 'test',
          ),
        );
      }
    
      Future<void> startPayment() async {
        final url = Uri.parse('http://localhost:4242/create-payment-intent');
        final response = await http.post(
          url,
          headers: {
            'Content-Type': 'application/json',
          },
          body: json.encode({
            'amount': 5000, // amount in cents
          }),
        );
    
        final paymentIntent = json.decode(response.body);
    
        final paymentMethod = await StripePayment.paymentRequestWithCardForm(
          CardFormPaymentRequest(),
        );
    
        final paymentIntentResult = await StripePayment.confirmPaymentIntent(
          PaymentIntent(
            clientSecret: paymentIntent['clientSecret'],
            paymentMethodId: paymentMethod.id,
          ),
        );
    
        if (paymentIntentResult.status == 'succeeded') {
          ScaffoldMessenger.of(context).showSnackBar(
            SnackBar(content: Text('Payment Successful!')),
          );
        } else {
          ScaffoldMessenger.of(context).showSnackBar(
            SnackBar(content: Text('Payment Failed!')),
          );
        }
      }
    
      @override
      Widget build(BuildContext context) {
        return Scaffold(
          appBar: AppBar(
            title: Text('Payment Gateway Integration'),
          ),
          body: Center(
            child: ElevatedButton(
              onPressed: startPayment,
              child: Text('Pay Now'),
            ),
          ),
        );
      }
    }
    ```
    
2. **Explanation:**
    
    * **Stripe Initialization:** We initialize Stripe with our publishable key.
        
    * **startPayment Method:** This method first calls our server to create a payment intent and get the client secret. Then, it opens a card form for the user to enter their payment details and confirm the payment.
        

## Running the App

1. **Run your Flutter app:**
    
    ```bash
    flutter run
    ```
    
2. **Test the payment:**
    
    * Enter test card details provided by Stripe (e.g., `4242 4242 4242 4242` with any future expiry date and CVC).
        
    * Confirm the payment and see if the transaction is successful.
        

## Conclusion

In this tutorial, we learned how to integrate Stripe as a payment gateway in a Flutter app. This involves setting up a server to handle payment intents, configuring Stripe in Flutter, and creating a simple UI for users to enter their payment details. With this foundation, you can extend the app to handle more complex payment scenarios and support additional features.