## Requirements

1. PWA
   - multi-language support
   - auth (login, register, forgot password)
     - first name, middle name, last name, email address, phone number, gender
     - google login & sign up
   - onboarding
     - class (A, B, C, D)
       - class name (A), description ( should be managed by administrator)
     - would you like to add a profile image?
     - state, zip code
     - Haven’t chosen School or Display No School
     - choose the Driving School according of state
       - should be displayed the logo and address ( should be managed by administrator or vender)
   - Acknowledge
     - Acknowledge: Yes or No
     - Would you like to be hired after graduation? Yes or No
     - When are you expected to take the exam for your CDL license? MM/DD/YYY - date-picker
   - Home
     - banner like “Welcome to the New Journey of your driving career!” (should be managed by administrator)
     - Progress status (0% completed)
   - Profile
     - What Nationality are you? (Nationalities should be managed by administrator)
     - Please upload resume
     - Upload Medical Card and Enter in Expiration Date
     - Upload Driver License and Enter in Expiration Date
     - Choose Endorsements ( should be managed by administrator) ( more details: requirements document)
     - Restrictions ( should be managed by administrator) ( more details: requirements document)
     - Reference type
     - Score sheet
2. Web Platform - Vendor
   1. Auth ( login )
      - Upon registration they can choose the different type of plans (programs)
   2. plans ( should be managed by administrator)
   3. dashboard
      - New applicant
      - Favorite Applicant
      - Hired Applicant
      - Archived applicant
      - restriction along with student status
      - restriction along with the payment type
   4. students list ( filtering, favorite)
   5. student detail ( set a status : Pending approval, background checked, hired, rejected, not hired)
   6. company profile
   7. Payment information setting
      - payment type: pay per profile,
   8. Checkout
      - one profile
      - multiple profiles at once
      - bulk actions at checkout
   9. Payment history
      - report generation
   10. job posting and advertising
3. Web Platform - Administrator (CRUD)
   1. Register applicant
   2. register new vendor
   3. add driving school
   4. add Class
   5. create QA for test and exam
   6. export & import data ( manual and automatic)
   7. RBAC
   8. add plans
   9. payment gateway management
   10. CMS ( pages management)
4. References
   1. https://play.google.com/store/apps/details?id=com.jeffreydiaz.android.app.cdlprep
   2. https://www.tenstreet.com/blog/driver-blog/cdl-endorsements-everything-you-need-to-know/
