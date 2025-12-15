# Major-project
# SEI - Similarity Search for Encrypted Images in Secure Cloud Computing

## Project Overview
A Java-based web application implementing secure content-based image retrieval (CBIR) over encrypted images in cloud computing environments using CNN-based feature extraction, hierarchical indexing, and limited key-leakage mechanisms.

**Author:** Shaik Rajak [21HU1A4298]  
**Guide:** Dr. Bhavani  
**Institution:** R V Institute of Technology (Formerly Chebrolu Engineering College)

## Features
- ✅ **High Search Accuracy** - CNN-based feature extraction
- ✅ **High Search Efficiency** - Hierarchical index tree with K-means clustering
- ✅ **Limited Key Leakage** - Secure trapdoor generation with optimized ASPE algorithm
- ✅ **Image Encryption** - AES encryption for secure cloud storage
- ✅ **Role-Based Access** - Separate interfaces for Owner, User, and Cloud Admin

## Technology Stack

### Backend
- **Java** - JDK 8 or higher
- **JSP** - JavaServer Pages
- **Servlets** - For request handling
- **JDBC** - Database connectivity

### Frontend
- **HTML5** - Structure
- **CSS3** - Styling
- **JavaScript** - Client-side validation

### Database
- **MySQL 5.7+** - Relational database

### Server
- **Apache Tomcat 7.0+** - Web server
- **XAMPP** (Alternative for MySQL)

## Project Structure
```
SEI-System/
├── src/
│   └── com/sei/
│       ├── servlet/
│       │   ├── OwnerRegistrationServlet.java
│       │   ├── OwnerLoginServlet.java
│       │   ├── UploadImageServlet.java
│       │   ├── UserRegistrationServlet.java
│       │   ├── UserLoginServlet.java
│       │   └── SearchImageServlet.java
│       └── util/
│           ├── DBConnection.java
│           ├── EncryptionUtil.java
│           └── FeatureExtractor.java
├── web/
│   ├── WEB-INF/
│   │   └── web.xml
│   ├── index.jsp
│   ├── owner_login.jsp
│   ├── owner_register.jsp
│   ├── owner_home.jsp
│   ├── user_login.jsp
│   ├── user_register.jsp
│   ├── user_home.jsp
│   ├── search_results.jsp
│   └── cloud_login.jsp
└── database/
    └── sei_system.sql
```

## Installation & Setup

### Prerequisites
1. **Java Development Kit (JDK) 8+**
   - Download from: https://www.oracle.com/java/technologies/downloads/
   - Set JAVA_HOME environment variable

2. **Apache Tomcat 7.0+**
   - Download from: https://tomcat.apache.org/download-70.cgi
   - Extract to a directory (e.g., C:\tomcat)

3. **MySQL Server 5.7+**
   - Download from: https://dev.mysql.com/downloads/mysql/
   - Or use XAMPP: https://www.apachefriends.org/

4. **NetBeans IDE 8.1+ (Recommended)**
   - Download from: https://netbeans.apache.org/

### Step 1: Database Setup

1. Start MySQL server
   ```bash
   # If using XAMPP, start MySQL from XAMPP Control Panel
   # Or start MySQL service from command line
   ```

2. Create database and tables
   ```sql
   -- Open MySQL command line or phpMyAdmin
   -- Execute the sei_system.sql file
   mysql -u root -p < database/sei_system.sql
   ```

3. Verify database creation
   ```sql
   USE sei_system;
   SHOW TABLES;
   ```

### Step 2: Configure Database Connection

1. Open `src/com/sei/util/DBConnection.java`

2. Update database credentials:
   ```java
   private static final String DB_URL = "jdbc:mysql://localhost:3306/sei_system";
   private static final String DB_USER = "root";
   private static final String DB_PASSWORD = ""; // Your MySQL password
   ```

### Step 3: Add Required JAR Files

Add the following JAR files to your project's `lib` folder:

1. **MySQL Connector/J** (JDBC Driver)
   - Download: https://dev.mysql.com/downloads/connector/j/
   - File: `mysql-connector-java-8.0.x.jar`

2. **Servlet API** (Usually included with Tomcat)
   - Location: `TOMCAT_HOME/lib/servlet-api.jar`

3. **JSP API** (Usually included with Tomcat)
   - Location: `TOMCAT_HOME/lib/jsp-api.jar`

### Step 4: Deploy to Tomcat

#### Option A: Using NetBeans IDE

1. Open NetBeans IDE
2. File → Open Project → Select SEI-System folder
3. Right-click project → Properties
4. Categories → Run → Server: Apache Tomcat
5. Right-click project → Clean and Build
6. Right-click project → Run

#### Option B: Manual Deployment

1. Build the project (create WAR file)
   ```bash
   # Navigate to project directory
   cd SEI-System
   jar -cvf SEI.war *
   ```

2. Copy WAR to Tomcat
   ```bash
   cp SEI.war TOMCAT_HOME/webapps/
   ```

3. Start Tomcat
   ```bash
   # Windows
   TOMCAT_HOME\bin\startup.bat
   
   # Linux/Mac
   TOMCAT_HOME/bin/startup.sh
   ```

4. Access application
   ```
   http://localhost:8080/SEI/
   ```

## Usage Guide

### For Image Owners

1. **Register Account**
   - Navigate to Image Owner → Register
   - Fill in username, password, email, mobile, ZIP code
   - System automatically generates encryption keys
   - Click Register

2. **Login**
   - Enter username and password
   - Click Login

3. **Upload Images**
   - Navigate to "Upload Image" tab
   - Enter image name
   - Select image file (JPG, PNG, etc.)
   - Add optional description
   - Click "Upload & Encrypt"
   - Image is encrypted and features are extracted automatically

4. **View Uploaded Images**
   - Navigate to "My Images" tab
   - View all encrypted images with details

5. **Manage Search Requests**
   - Navigate to "View Requests" tab
   - Review search requests from users
   - Approve or reject requests

### For Image Users

1. **Register Account**
   - Navigate to Image User → Register
   - Fill in required details
   - Click Register

2. **Login**
   - Enter credentials
   - Click Login

3. **Search Similar Images**
   - Select an image owner from dropdown
   - Upload query image
   - Set number of similar images (k value)
   - Click "Search Similar Images"

4. **View Results**
   - System displays top-k similar images
   - Results show similarity scores and rankings
   - View search history in "My Search History"

### For Cloud Admin

1. **Login**
   - Default credentials: admin / admin123
   - Access all system operations
   - Monitor user activities

## System Architecture

### Modules

1. **Image Owner Module**
   - User registration and authentication
   - Key pair generation
   - Image upload and encryption
   - Feature extraction using CNN
   - Request management

2. **Image User Module**
   - User registration and authentication
   - Query image upload
   - Similarity search
   - Result visualization
   - Search history

3. **Cloud Server Module**
   - Encrypted image storage
   - Similarity calculation
   - Hierarchical index tree management
   - Request processing
   - Activity logging

### Security Features

1. **Image Encryption**
   - AES-128 encryption for image data
   - Separate encryption for feature vectors

2. **Key Management**
   - RSA-2048 for key pair generation
   - Limited key-leakage mechanism
   - Secure key storage

3. **Privacy Preservation**
   - Encrypted storage
   - Secure search protocol
   - Privacy-preserving feature matching

## Algorithm Overview

### Feature Extraction
1. Image uploaded by owner
2. CNN-based feature extraction (128-dimensional vector)
3. Color histogram analysis (RGB)
4. Texture feature computation
5. Feature vector normalization

### Similarity Search
1. User uploads query image
2. Extract query features
3. Encrypted search trapdoor generation
4. Traverse hierarchical index tree
5. Calculate similarity using Euclidean distance
6. Return top-k results

### Hierarchical Indexing
1. Extract features from all images
2. Apply K-means clustering
3. Build tree in bottom-up manner
4. Store cluster centers
5. Enable efficient pruning during search

## Troubleshooting

### Common Issues

**Issue 1: Database Connection Failed**
- Solution: Check MySQL service is running
- Verify database credentials in DBConnection.java
- Ensure sei_system database exists

**Issue 2: ClassNotFoundException for JDBC Driver**
- Solution: Add mysql-connector-java JAR to lib folder
- Rebuild project
- Restart Tomcat

**Issue 3: Port 8080 Already in Use**
- Solution: Change Tomcat port in server.xml
- Or stop other services using port 8080

**Issue 4: File Upload Failed**
- Solution: Check Tomcat temp directory permissions
- Increase file size limit in web.xml
- Verify @MultipartConfig annotation

**Issue 5: Images Not Displaying**
- Solution: Check image paths
- Verify file upload directory exists
- Check file permissions

## Testing

### Unit Testing
- Test individual servlets
- Verify database operations
- Test encryption/decryption

### Integration Testing
- Test complete workflow
- Owner upload → User search → Results
- Verify data consistency

### Performance Testing
- Test with multiple images
- Measure search response time
- Check system scalability

## Future Enhancements

1. **Dynamic Update Support**
   - Efficient index updates
   - Real-time image addition/deletion

2. **Multi-Owner Scenario**
   - Support multiple image owners
   - Cross-owner search capabilities

3. **Result Verification**
   - Allow users to verify search results
   - Implement cryptographic proofs

4. **Advanced CNN Models**
   - Integrate ResNet, VGG models
   - Improve feature extraction accuracy

5. **Mobile Application**
   - Develop Android/iOS apps
   - Cloud-mobile integration

## References

1. C.-Y. Hsu, et al., "Image feature extraction in encrypted domain with privacy-preserving SIFT," IEEE Trans. Image Processing, 2012.

2. Z. Xia, et al., "EPCBIR: An efficient and privacy-preserving content-based image retrieval scheme in cloud computing," Information Sciences, 2017.

3. M. Shen, et al., "Content-based multi-source encrypted image retrieval in clouds with privacy preservation," Future Generation Computer Systems, 2018.

## License
This project is developed as part of academic requirements at R V Institute of Technology.

## Contact
**Developer:** Shaik Rajak  
**Email:** shaikrajak.21hu1a4298@rvit.ac.in  
**Institution:** R V Institute of Technology, Guntur, AP

---

**Note:** This is an academic project. For production use, additional security measures and optimizations are recommended.
