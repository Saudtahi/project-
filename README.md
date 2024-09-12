# More Than Just A Lunch - Web Application

## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Running the App Locally](#running-the-app-locally)
  - [API Integration](#api-integration)
    - [Adding a Verified Email Address](#adding-a-verified-email-address)
- [Deployment](#deployment)
  - [Deploying to Vercel](#deploying-to-vercel)
- [License](#license)
- [Contributing](#contributing)
- [Contact](#contact)

## Introduction

Welcome to **More Than Just A Lunch**, a vibrant platform designed to foster connections and promote meaningful events. This web application is your gateway to discovering our mission, exploring upcoming events, and engaging with a community that believes in the power of gathering around a meal.

## Features

- **Dynamic Image Slideshow**: Captivating visuals on the homepage that set the tone for the experience.
- **Impactful Messaging**: A strong, clear message that resonates with the values of our community.
- **Easy Navigation**: Quick access to event registration, information about our mission, and user testimonials.
- **Email Integration**: Seamless communication through our integration with the Mailjet API.

## Technologies Used

- **Next.js**: A powerful React framework for building modern web applications.
- **React**: A JavaScript library for crafting interactive user interfaces.
- **Tailwind CSS**: A utility-first CSS framework for sleek and responsive designs.
- **Mailjet**: A robust email API service for handling all our communication needs.
- **Vercel**: A platform for smooth deployment and scaling of our web application.

## Getting Started

### Prerequisites

Ensure your development environment is ready with the following tools:

- Node.js (v14.x or later)
- npm (v9.6.7 or later) or yarn (v1.22.19 or later)
- Git

### Installation

1. **Set Node Version**:
   Before installing dependencies, set your Node.js version to 18.17.0 using nvm:
   ```bash
   nvm use 18.17.0
   ```

2. **Install Dependencies**:
   Using npm:
   ```bash
   npm install
   ```
   Or using yarn:
   ```bash
   yarn install
   ```

### Running the App Locally

1. **Set Up Environment Variables**:
   Create a `.env.local` file in the root directory of the project and add the following environment variable:
   ```bash
   MJ_APIKEY_PUBLIC=your-mailjet-public-api-key
   MJ_APIKEY_PRIVATE=your-mailjet-private-api-key
   ```

2. **Start the Development Server**:
   Using npm:
   ```bash
   npm run dev
   ```
   Or using yarn:
   ```bash
   yarn dev
   ```
   The app should now be accessible at `http://localhost:3000`.

### API Integration

This application leverages **Mailjet** for email communication. Here’s how to set it up:

1. **Create a Mailjet Account**:
   - Sign up at [Mailjet](https://www.mailjet.com/).
   - Once signed up, navigate to the API keys section in your Mailjet dashboard.

2. **Generate an API Key**:
   - Create an API key with appropriate permissions.
   - Add the API keys to your `.env.local` file:
     ```bash
     MJ_APIKEY_PUBLIC=your-mailjet-public-api-key
     MJ_APIKEY_PRIVATE=your-mailjet-private-api-key
     ```

3. **Integrate the API Key**:
   - The `MJ_APIKEY_PUBLIC` and `MJ_APIKEY_PRIVATE` environment variables will be used in your Next.js API routes to enable email sending functionality.

#### Adding a Verified Email Address

For Mailjet to send emails on your behalf, you need to add a verified sender email address in the `send-email.js` file. Here’s how to do it:

1. **Verify Your Email Address**:
   - In your Mailjet dashboard, navigate to "Sender Addresses" and follow the steps to verify your sender email address.

2. **Update the `send-email.js` File**:
   - Locate the `send-email.js` file in your Next.js project under the `/pages/api/` directory.
   - Modify the email sending code as follows:
     ```javascript
     import mailjet from 'node-mailjet';

     const mj = mailjet.apiConnect(process.env.MJ_APIKEY_PUBLIC, process.env.MJ_APIKEY_PRIVATE);

     export default async function handler(req, res) {
       try {
         const request = mj
           .post("send", { version: 'v3.1' })
           .request({
             Messages: [
               {
                 From: {
                   Email: 'your-verified-email@example.com',
                   Name: 'Your Name'
                 },
                 To: [
                   {
                     Email: 'someEmailAnyEmail@me.com',
                     Name: 'Recipient Name'
                   }
                 ],
                 Subject: 'More Than a Lunch Sign up Request Form',
                 TextPart: 'Thank you for signing up for More Than a Lunch!',
                 HTMLPart: '<strong>Thank you for signing up for More Than a Lunch!</strong>'
               }
             ]
           });

         const result = await request;
         console.log('Email sent:', result.body);
         res.status(200).json({ message: 'Email sent successfully' });
       } catch (error) {
         console.error(error);
         res.status(500).json({ message: 'Failed to send email' });
       }
     }
     ```

3. **Test the Email Sending**:
   - Run your application locally and ensure that emails are being sent successfully using your verified email address.

## Deployment

### Deploying to Vercel

1. **Sign Up or Log In to Vercel**:
   - Visit [Vercel](https://vercel.com/) and sign up or log in.

2. **Connect Your GitHub Repository**:
   - From the Vercel dashboard, click on "New Project" and import your GitHub repository.

3. **Configure Environment Variables**:
   - In the Vercel dashboard, navigate to your project settings and add your environment variables, including the `MJ_APIKEY_PUBLIC` and `MJ_APIKEY_PRIVATE`.

4. **Deploy**:
   - Once connected and configured, click "Deploy".
   - Vercel will build and deploy your application, and you’ll be provided with a live URL.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for more details.

## Contributing

We welcome contributions! Whether it’s a bug fix, a new feature, or an improvement, feel free to submit a Pull Request or open an Issue.

## Contact

For inquiries or support, please reach out to Istafa at istafamarshall@me.com.

---

**More Than Just A Lunch** is more than an application; it's a movement that brings people together. With this platform, we hope to continue fostering connections and creating memorable experiences around the table. Thank you for being part of our journey!

---
