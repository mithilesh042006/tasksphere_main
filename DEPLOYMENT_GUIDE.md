# 🚀 TaskSphere Deployment Guide

## 🔧 Configuration Fixes Applied

### **Django Backend Configuration**

**ALLOWED_HOSTS Update**
The Django settings have been updated to allow connections from various development environments:

```python
# tasksphere_backend/tasksphere_backend/settings.py
ALLOWED_HOSTS = [
    'localhost',
    '127.0.0.1',
    '10.0.2.2',  # Android emulator
    '0.0.0.0',   # Allow all interfaces
    '*',         # Allow all hosts (development only)
]
```

### **Flutter Frontend Configuration**

**Dynamic API Base URL**
The API client now automatically selects the correct base URL based on the platform:

```dart
// tasksphere_frontend/lib/services/api_client.dart
static String get baseUrl {
  if (kIsWeb) {
    // Web platform
    return 'http://127.0.0.1:8000';
  } else if (Platform.isAndroid) {
    // Android emulator
    return 'http://10.0.2.2:8000';
  } else if (Platform.isIOS) {
    // iOS simulator
    return 'http://127.0.0.1:8000';
  } else {
    // Desktop platforms
    return 'http://127.0.0.1:8000';
  }
}
```

## 📱 Platform-Specific Setup

### **Web Development**
```bash
# Backend
cd tasksphere_backend
python manage.py runserver

# Frontend
cd tasksphere_frontend
flutter run -d chrome
```
**API URL**: `http://127.0.0.1:8000`

### **Android Development**
```bash
# Backend
cd tasksphere_backend
python manage.py runserver

# Frontend (with Android emulator running)
cd tasksphere_frontend
flutter run
```
**API URL**: `http://10.0.2.2:8000`

### **iOS Development**
```bash
# Backend
cd tasksphere_backend
python manage.py runserver

# Frontend (with iOS simulator running)
cd tasksphere_frontend
flutter run
```
**API URL**: `http://127.0.0.1:8000`

### **Physical Device Development**
For testing on physical devices, you'll need to:

1. **Find your computer's IP address**:
   ```bash
   # Windows
   ipconfig
   
   # macOS/Linux
   ifconfig
   ```

2. **Update the API client** to use your computer's IP:
   ```dart
   // Add this case in the baseUrl getter
   return 'http://YOUR_COMPUTER_IP:8000';
   ```

3. **Update Django ALLOWED_HOSTS**:
   ```python
   ALLOWED_HOSTS = [
       'localhost',
       '127.0.0.1',
       '10.0.2.2',
       'YOUR_COMPUTER_IP',  # Add your IP here
       '*',
   ]
   ```

## 🔒 Production Deployment

### **Backend (Django)**

**Security Settings**:
```python
# For production, update these settings:
DEBUG = False
ALLOWED_HOSTS = ['your-domain.com', 'api.your-domain.com']

# Add proper database configuration
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'tasksphere_prod',
        'USER': 'your_user',
        'PASSWORD': 'your_password',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}

# Add proper static files configuration
STATIC_ROOT = '/path/to/static/files'
MEDIA_ROOT = '/path/to/media/files'
```

**Deployment Options**:
- **Heroku**: Use `gunicorn` and PostgreSQL
- **DigitalOcean**: Use Docker with nginx
- **AWS**: Use Elastic Beanstalk or EC2
- **Railway**: Simple deployment with PostgreSQL

### **Frontend (Flutter)**

**Web Deployment**:
```bash
flutter build web --release
# Deploy the build/web folder to your hosting service
```

**Mobile App Deployment**:
```bash
# Android
flutter build apk --release
flutter build appbundle --release

# iOS
flutter build ios --release
```

**Update API URL for Production**:
```dart
static String get baseUrl {
  if (kIsWeb) {
    return 'https://your-api-domain.com';
  } else {
    return 'https://your-api-domain.com';
  }
}
```

## 🧪 Testing

### **Backend Testing**
```bash
cd tasksphere_backend
python manage.py test
```

### **Frontend Testing**
```bash
cd tasksphere_frontend
flutter test
```

### **API Testing**
Use the provided `test_api.py` script:
```bash
cd tasksphere_backend
python test_api.py
```

## 🔍 Troubleshooting

### **Common Issues**

1. **CORS Errors**:
   - Ensure `django-cors-headers` is installed and configured
   - Check `CORS_ALLOWED_ORIGINS` in Django settings

2. **Authentication Errors**:
   - Verify JWT tokens are being stored correctly
   - Check token expiration settings

3. **Network Errors**:
   - Verify the correct API URL for your platform
   - Check firewall settings
   - Ensure Django server is running

4. **Build Errors**:
   - Run `flutter clean` and `flutter pub get`
   - Check for dependency conflicts

### **Debug Commands**
```bash
# Flutter
flutter doctor
flutter clean
flutter pub deps

# Django
python manage.py check
python manage.py showmigrations
python manage.py collectstatic
```

## 📊 Performance Optimization

### **Backend**
- Use Redis for caching
- Implement database indexing
- Use pagination for large datasets
- Optimize database queries

### **Frontend**
- Implement lazy loading
- Use cached network images
- Optimize build size
- Implement offline support

---

**🎉 TaskSphere is now properly configured for all platforms!** 🚀
