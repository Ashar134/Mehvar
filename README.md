# 🏗️ Mehvar – A Smarter Way to Build!

**Mehvar** is a web-based construction project bidding platform developed as part of a 6th semester Web Engineering course. Our platform bridges the gap between clients and builders by enabling efficient, transparent collaboration for construction projects.

---

## 🚀 Features

- **Post & Bid System**  
  Clients can post construction projects, and builders can submit competitive bids based on price, timeline, and ratings.

- **Transparent Bidding**  
  Builders compete openly, ensuring the best value and service for clients.

-  **Review & Ratings**  
  Clients and builders can leave reviews after project completion, fostering trust and accountability.

- **Material Marketplace**  
  A real-time marketplace showcasing construction accessories and materials.

- **User Profile Management**  
  Customizable profiles for both clients and builders.

- **Secure Payments**  
  Stripe API integration for secure and seamless transactions.

---

## Built With

- **Backend:** Python (Flask)
- **Frontend:** HTML, CSS
- **Database:** MySQL
- **Payment Integration:** Stripe API

---

### Installation  
1. **Clone the repository**  
   ```sh
   git clone https://github.com/Ashar134/Mehvar.git
   cd Mehvar

---

### Database Setup (MySQL)
You can import the entire database (tables + sample data) NOTE : the database must be in the project directory or at the place where you are making your database.
```sh
mysql -u root -p -e "CREATE DATABASE ClickNBuild;
USE ClickNBuild; 
SOURCE ClickNBuild.sql;"
