# StudyNotion Environment Setup Guide

This guide will help you set up the environment variables for both the frontend and backend of the StudyNotion project.

## 📁 File Structure

You need to create two `.env` files:

1. **Root directory**: `.env` (for frontend)
2. **Server directory**: `server/.env` (for backend)

## 🎯 Frontend Environment Variables

Create a `.env` file in the root directory:

```env
# Frontend Environment Variables
REACT_APP_BASE_URL=http://localhost:4000/api/v1
REACT_APP_STRIPE_PUBLISHABLE_KEY=your_stripe_publishable_key_here
```

## 🔧 Backend Environment Variables

Create a `.env` file in the `server/` directory:

```env
# Backend Environment Variables

# Server Configuration
PORT=4000

# Database Configuration
MONGODB_URL=mongodb://localhost:27017/studynotion

# JWT Configuration
JWT_SECRET=your_jwt_secret_key_here

# Cloudinary Configuration (for file uploads)
CLOUD_NAME=your_cloudinary_cloud_name
API_KEY=your_cloudinary_api_key
API_SECRET=your_cloudinary_api_secret
FOLDER_NAME=studynotion

# Stripe Configuration (for payments)
STRIPE_SECRET_KEY=your_stripe_secret_key
STRIPE_WEBHOOK_SECRET=your_stripe_webhook_secret

# Email Configuration (for nodemailer)
MAIL_HOST=smtp.gmail.com
MAIL_USER=your_email@gmail.com
MAIL_PASS=your_email_app_password
```

## 🔑 How to Get These Values

### 1. **MongoDB Setup**
- Install MongoDB locally or use MongoDB Atlas
- For local: `MONGODB_URL=mongodb://localhost:27017/studynotion`
- For Atlas: `MONGODB_URL=mongodb+srv://username:password@cluster.mongodb.net/studynotion`

### 2. **JWT Secret**
- Generate a strong, random string for `JWT_SECRET`

### 3. **Cloudinary Setup**
1. Go to [Cloudinary](https://cloudinary.com/)
2. Create a free account
3. Get your `Cloud Name`, `API Key`, and `API Secret` from the dashboard

### 4. **Stripe Setup**
1. Go to [Stripe](https://stripe.com/)
2. Navigate to the **Developers** section
3. In the **API keys** tab, you will find your keys:
   - **Publishable key**: Use this for `REACT_APP_STRIPE_PUBLISHABLE_KEY` in the frontend `.env`
   - **Secret key**: Use this for `STRIPE_SECRET_KEY` in the backend `server/.env`
4. **Webhook Secret**:
   - To test your webhook locally, you'll need the [Stripe CLI](https://stripe.com/docs/stripe-cli)
   - Run `stripe listen --forward-to localhost:4000/api/v1/payment/verifyPayment`
   - The CLI will output a webhook signing secret (e.g., `whsec_...`). Use this for `STRIPE_WEBHOOK_SECRET`

### 5. **Email Setup (Gmail)**
1. Enable 2-factor authentication on your Gmail account
2. Generate an **App Password** in your Google Account security settings
3. Use your Gmail address for `MAIL_USER` and the generated app password for `MAIL_PASS`

## 🚀 Quick Setup Commands

```bash
# Create frontend .env file
echo "REACT_APP_BASE_URL=http://localhost:4000/api/v1
REACT_APP_STRIPE_PUBLISHABLE_KEY=your_stripe_publishable_key_here" > .env

# Create backend .env file
echo "PORT=4000
MONGODB_URL=mongodb://localhost:27017/studynotion
JWT_SECRET=your_jwt_secret_key_here
CLOUD_NAME=your_cloudinary_cloud_name
API_KEY=your_cloudinary_api_key
API_SECRET=your_cloudinary_api_secret
FOLDER_NAME=studynotion
STRIPE_SECRET_KEY=your_stripe_secret_key
STRIPE_WEBHOOK_SECRET=your_stripe_webhook_secret
MAIL_HOST=smtp.gmail.com
MAIL_USER=your_email@gmail.com
MAIL_PASS=your_email_app_password" > server/.env
```

## ⚠️ Important Notes

1. **Never commit `.env` files** to version control
2. **Keep your secrets secure** and don't share them publicly
3. **For production, use live keys from Stripe** and a more robust email service

## 🔍 Verification

After setting up the environment variables:

1. **Start the backend**: `cd server && npm run dev`
2. **Start the frontend**: `npm start`
3. **Test user signup and course creation**: Check if the user signup and course creation processes work
4. **Test the payment flow with Stripe's test card numbers**: Use Stripe's test card numbers to test the payment flow
5. **Check that the webhook successfully enrolls the student**: Ensure that the webhook successfully enrolls the student when a payment is made

## 🆘 Troubleshooting

### Common Issues:

1. **"Stripe checkout failed"**: Verify your Publishable and Secret keys are correct
2. **"Webhook verification failed"**: Ensure the `STRIPE_WEBHOOK_SECRET` is correct and that the Stripe CLI is forwarding to the right port
3. **"Email sending failed"**: Check your Gmail App Password

## 📞 Support

If you encounter any issues, check:
1. All environment variables are set correctly
2. All services (MongoDB, Cloudinary, Stripe) are accessible
3. Network connectivity for external services 