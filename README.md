# Travel4Fun


## **1. Tools and Technologies**
Here’s a list of tools and technologies you’ll need:

### **Frontend (Blazor Web App)**
- **Blazor WebAssembly** or **Blazor Server**: For building the interactive UI.
- **ASP.NET Core**: For backend APIs and server-side logic.
- **Razor Components**: For reusable UI components.
- **Bootstrap** or **Tailwind CSS**: For styling the app.
- **JavaScript Interop**: For integrating JavaScript libraries (if needed).

### **Backend**
- **ASP.NET Core Web API**: For handling business logic and serving data to the frontend.
- **Entity Framework Core**: For database interactions (ORM).
- **SQL Server** or **PostgreSQL**: For storing user, host, and experience data.
- **Authentication**: Use **ASP.NET Core Identity** or **Auth0** for user authentication.

### **Hosting**
- **Frontend Hosting**:
  - **Azure Static Web Apps**: Great for hosting Blazor WebAssembly apps.
  - **Netlify** or **Vercel**: Alternative hosting options.
- **Backend Hosting**:
  - **Azure App Service**: For hosting ASP.NET Core APIs.
  - **AWS Elastic Beanstalk** or **Google Cloud Run**: Alternatives.
- **Database Hosting**:
  - **Azure SQL Database**: For SQL Server.
  - **ElephantSQL**: For PostgreSQL.

### **Other Tools**
- **GitHub/GitLab**: For version control.
- **Docker**: For containerizing the app (optional but recommended).
- **Swagger/OpenAPI**: For API documentation.
- **Stripe API**: For payment processing (if you plan to monetize experiences).

---

## **2. Database Design**
Here’s a basic database schema for your app:

### **Tables**
1. **Users**:
   - `UserId` (Primary Key)
   - `Username`
   - `Email`
   - `PasswordHash`
   - `Role` (Traveler or Host)
   - `ProfilePictureUrl`
   - `Bio`

2. **Experiences**:
   - `ExperienceId` (Primary Key)
   - `HostId` (Foreign Key to Users)
   - `Title` (e.g., "Make your own Asado")
   - `Description`
   - `Location` (e.g., "Buenos Aires, Argentina")
   - `Price`
   - `Duration` (e.g., "3 hours")
   - `MaxParticipants`
   - `ImageUrl`

3. **Bookings**:
   - `BookingId` (Primary Key)
   - `TravelerId` (Foreign Key to Users)
   - `ExperienceId` (Foreign Key to Experiences)
   - `BookingDate`
   - `Status` (e.g., "Pending", "Confirmed", "Cancelled")

4. **Reviews**:
   - `ReviewId` (Primary Key)
   - `ExperienceId` (Foreign Key to Experiences)
   - `TravelerId` (Foreign Key to Users)
   - `Rating` (e.g., 1-5 stars)
   - `Comment`

---

## **3. App Structure and Pages**
Here’s a breakdown of the pages and their functionality:

### **1. Home Page**
- Displays a feed of all available experiences.
- Includes a search bar to filter experiences by location, price, or category.
- Each experience card shows:
  - Title
  - Host name
  - Location
  - Price
  - Rating (if available)
  - "Book Now" button.

### **2. Experience Detail Page**
- Shows detailed information about a specific experience:
  - Title
  - Description
  - Host profile
  - Location
  - Price
  - Duration
  - Reviews
  - "Book Now" button.

### **3. Host Dashboard**
- Allows hosts to:
  - Create new experiences.
  - Edit existing experiences.
  - View bookings for their experiences.
  - Manage their profile.

### **4. Traveler Dashboard**
- Allows travelers to:
  - View their booked experiences.
  - Leave reviews.
  - Manage their profile.

### **5. Authentication Pages**
- **Login Page**: For users to log in.
- **Register Page**: For new users to sign up (as travelers or hosts).

---

## **4. Step-by-Step Development Plan**

### **Step 1: Set Up the Project**
1. Install **.NET SDK**.
2. Create a new Blazor WebAssembly project:
   ```bash
   dotnet new blazorwasm -n TravelLocalApp
   ```
3. Add an ASP.NET Core Web API project for the backend:
   ```bash
   dotnet new webapi -n TravelLocalApp.API
   ```

### **Step 2: Set Up the Database**
1. Install **Entity Framework Core**:
   ```bash
   dotnet add package Microsoft.EntityFrameworkCore.SqlServer
   ```
2. Create the database context and models (e.g., `User`, `Experience`, `Booking`, `Review`).
3. Run migrations to create the database:
   ```bash
   dotnet ef migrations add InitialCreate
   dotnet ef database update
   ```

### **Step 3: Implement Authentication**
1. Use **ASP.NET Core Identity** for user authentication.
2. Add login and registration pages in Blazor.
3. Secure API endpoints using JWT tokens.

### **Step 4: Build the Frontend**
1. Create reusable Razor components (e.g., `ExperienceCard.razor`, `NavMenu.razor`).
2. Use **Bootstrap** for styling.
3. Fetch data from the backend API using `HttpClient`.

### **Step 5: Implement Host and Traveler Dashboards**
1. Create separate views for hosts and travelers.
2. Allow hosts to create and manage experiences.
3. Allow travelers to book experiences and leave reviews.

### **Step 6: Deploy the App**
1. Deploy the Blazor frontend to **Azure Static Web Apps**.
2. Deploy the backend API to **Azure App Service**.
3. Set up the database on **Azure SQL Database**.

---

## **5. Additional Ideas**
- **Social Sharing**: Allow travelers to share their booked experiences on social media.
- **Chat Feature**: Add a chat system for travelers and hosts to communicate.
- **Local Recommendations**: Use geolocation to recommend nearby experiences.
- **Multilingual Support**: Add support for multiple languages.

---
