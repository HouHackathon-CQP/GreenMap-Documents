# Installation Guide

This guide will help you set up GreenMap on your local machine or deploy it to a server.

## Prerequisites

Before you begin, ensure you have the following installed:

- **Python** 3.8 or higher
- **Node.js** 14.x or higher
- **Git** for version control
- A modern web browser (Chrome, Firefox, Safari, or Edge)

## Installation Methods

### Method 1: Quick Install (Recommended)

The quickest way to get started with GreenMap:

```bash
# Clone the repository
git clone https://github.com/HouHackathon-CQP/GreenMap.git
cd GreenMap

# Install dependencies
npm install

# Start the development server
npm start
```

### Method 2: Manual Installation

For more control over the installation process:

#### Step 1: Clone the Repository

```bash
git clone https://github.com/HouHackathon-CQP/GreenMap.git
cd GreenMap
```

#### Step 2: Install Backend Dependencies

```bash
cd backend
pip install -r requirements.txt
```

#### Step 3: Install Frontend Dependencies

```bash
cd ../frontend
npm install
```

#### Step 4: Configure Environment Variables

Create a `.env` file in the root directory:

```bash
cp .env.example .env
```

Edit the `.env` file with your configuration:

```env
DATABASE_URL=your_database_url
API_KEY=your_api_key
PORT=3000
```

#### Step 5: Initialize the Database

```bash
cd backend
python manage.py migrate
```

#### Step 6: Start the Application

```bash
# Start backend (in one terminal)
cd backend
python manage.py runserver

# Start frontend (in another terminal)
cd frontend
npm start
```

## Docker Installation

For containerized deployment:

```bash
# Clone the repository
git clone https://github.com/HouHackathon-CQP/GreenMap.git
cd GreenMap

# Build and run with Docker Compose
docker-compose up -d
```

## Verifying Your Installation

After installation, verify that GreenMap is running:

1. Open your browser and navigate to `http://localhost:3000`
2. You should see the GreenMap homepage
3. Try creating a test account to ensure the backend is working

## Troubleshooting

### Common Issues

#### Port Already in Use

If port 3000 is already in use:

```bash
# Change the port in your .env file
PORT=8080
```

#### Database Connection Error

Ensure your database is running and the connection string is correct:

```bash
# Check database status
systemctl status postgresql
```

#### Missing Dependencies

If you encounter missing dependency errors:

```bash
# Clear npm cache and reinstall
npm cache clean --force
rm -rf node_modules
npm install
```

## System Requirements

### Minimum Requirements

- **CPU**: Dual-core processor
- **RAM**: 4 GB
- **Storage**: 10 GB free space
- **OS**: Windows 10, macOS 10.14+, or Linux

### Recommended Requirements

- **CPU**: Quad-core processor
- **RAM**: 8 GB or more
- **Storage**: 20 GB free space
- **OS**: Latest version of Windows, macOS, or Linux

## Next Steps

Now that you have GreenMap installed:

- Follow the [Quick Start Guide](quick-start.md) to learn the basics
- Explore the [User Guide](../user-guide/overview.md) for detailed features
- Check out the [API Reference](../api-reference/overview.md) if you're a developer

## Getting Help

If you encounter issues during installation:

- Check our [FAQ](../user-guide/features.md#faq)
- Visit our GitHub [Issues](https://github.com/HouHackathon-CQP/GreenMap/issues) page
- Join our community Discord server

---

*Ready to make a difference? Let's get started!*
