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


-----------------------------

#Step by Step:

---

## **Step-by-Step Guide to Build Your Travel4Fun App**

### **1. Project Setup (Already Done)**
You’ve already completed this step, but here’s a recap:
- Open Visual Studio Code (or Visual Studio).
- Create a new Blazor Web App:
  - Select **Blazor Web App** as the project type.
  - Name it **Travel4Fun**.
  - Choose **.NET 9.0** as the framework.
  - Select **Blazor WebAssembly** (or Blazor Server, depending on your preference).

---

### **2. Decide if You Need a Web API**
Yes, you will need a **Web API** for the following reasons:
- **Backend Logic**: To handle database operations, authentication, and business logic.
- **Separation of Concerns**: Keeps your frontend (Blazor) and backend (API) independent.
- **Scalability**: Makes it easier to scale the app in the future.

---

### **3. Create the Web API Project**
1. Open your terminal in the **Travel4Fun** solution folder.
2. Create a new ASP.NET Core Web API project:
   ```bash
   dotnet new webapi -n Travel4Fun.API
   ```
3. Add the Web API project to your solution:
   ```bash
   dotnet sln add Travel4Fun.API
   ```

---

### **4. Set Up the Database**
1. Install **Entity Framework Core**:
   ```bash
   dotnet add package Microsoft.EntityFrameworkCore.SqlServer
   dotnet add package Microsoft.EntityFrameworkCore.Design
   ```
2. Create your database models (e.g., `User`, `Experience`, `Booking`, `Review`).
   - Example `User` model:
     ```csharp
     public class User
     {
         public int UserId { get; set; }
         public string Username { get; set; }
         public string Email { get; set; }
         public string PasswordHash { get; set; }
         public string Role { get; set; } // Traveler or Host
     }
     ```
3. Create a `DbContext` class:
   ```csharp
   public class Travel4FunDbContext : DbContext
   {
       public DbSet<User> Users { get; set; }
       public DbSet<Experience> Experiences { get; set; }
       public DbSet<Booking> Bookings { get; set; }
       public DbSet<Review> Reviews { get; set; }

       public Travel4FunDbContext(DbContextOptions<Travel4FunDbContext> options) : base(options) { }
   }
   ```
4. Add the connection string to `appsettings.json`:
   ```json
   "ConnectionStrings": {
       "DefaultConnection": "Server=your_server;Database=Travel4FunDb;Trusted_Connection=True;"
   }
   ```
5. Run migrations to create the database:
   ```bash
   dotnet ef migrations add InitialCreate
   dotnet ef database update
   ```

---

### **5. Set Up Authentication**
1. Install **ASP.NET Core Identity**:
   ```bash
   dotnet add package Microsoft.AspNetCore.Identity.EntityFrameworkCore
   ```
2. Configure Identity in `Startup.cs` or `Program.cs`:
   ```csharp
   builder.Services.AddIdentity<User, IdentityRole>()
       .AddEntityFrameworkStores<Travel4FunDbContext>()
       .AddDefaultTokenProviders();
   ```
3. Add authentication middleware:
   ```csharp
   builder.Services.AddAuthentication();
   builder.Services.AddAuthorization();
   ```

---

### **6. Create API Endpoints**
1. Create controllers for your API (e.g., `ExperiencesController`, `UsersController`).
   - Example `ExperiencesController`:
     ```csharp
     [ApiController]
     [Route("api/[controller]")]
     public class ExperiencesController : ControllerBase
     {
         private readonly Travel4FunDbContext _context;

         public ExperiencesController(Travel4FunDbContext context)
         {
             _context = context;
         }

         [HttpGet]
         public async Task<ActionResult<IEnumerable<Experience>>> GetExperiences()
         {
             return await _context.Experiences.ToListAsync();
         }
     }
     ```

---

### **7. Integrate the API with Blazor**
1. In your Blazor app, add a service to call the API:
   ```csharp
   public class ExperienceService
   {
       private readonly HttpClient _httpClient;

       public ExperienceService(HttpClient httpClient)
       {
           _httpClient = httpClient;
       }

       public async Task<List<Experience>> GetExperiencesAsync()
       {
           return await _httpClient.GetFromJsonAsync<List<Experience>>("api/experiences");
       }
   }
   ```
2. Register the service in `Program.cs`:
   ```csharp
   builder.Services.AddScoped<ExperienceService>();
   builder.Services.AddHttpClient();
   ```

---

### **8. Build the Frontend**
1. Create Razor components for your pages (e.g., `Home.razor`, `ExperienceDetail.razor`).
2. Fetch data from the API in your components:
   ```razor
   @page "/"
   @inject ExperienceService ExperienceService

   <h3>Experiences</h3>
   <ul>
       @foreach (var experience in experiences)
       {
           <li>@experience.Title</li>
       }
   </ul>

   @code {
       private List<Experience> experiences;

       protected override async Task OnInitializedAsync()
       {
           experiences = await ExperienceService.GetExperiencesAsync();
       }
   }
   ```

---

### **9. Deploy the App**
1. Deploy the Blazor app to **Azure Static Web Apps**.
2. Deploy the API to **Azure App Service**.
3. Set up the database on **Azure SQL Database**.

---

### **10. Additional Features**
- **Search and Filters**: Add search and filter functionality to the home page.
- **Reviews and Ratings**: Allow travelers to leave reviews for experiences.
- **Payment Integration**: Use **Stripe API** for booking payments.

---
