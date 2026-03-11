# InventoryHub

A comprehensive inventory management system built with Flask and SQLAlchemy. InventoryHub helps businesses track items, manage stock levels, and analyze inventory metrics with an intuitive web interface and AI-powered chatbot support.

## Features

- **User Authentication**: Secure registration and login with password hashing
- **Inventory Management**: Create, update, and delete items with detailed properties
- **Item Groups**: Organize items into groups with custom attributes
- **Dashboard Analytics**: Real-time inventory metrics including:
  - Total inventory value
  - Low stock alerts
  - Item type distribution
  - Margin analysis
  - Tax distribution tracking
- **Admin Dashboard**: Comprehensive system overview for administrators
  - User management
  - Inventory statistics
  - Price distribution analysis
  - Recent activity tracking
- **AI Chatbot**: Integrated chatbot for intelligent inventory queries
- **Responsive UI**: Clean, modern interface with CSS and JavaScript
- **Role-based Access Control**: Admin and user roles with different permissions
- **Profile Management**: User profiles with change password functionality

## Technology Stack

- **Backend**: Python Flask, Flask-SQLAlchemy
- **Database**: SQLite
- **Frontend**: HTML5, CSS3, JavaScript
- **Security**: Werkzeug password hashing
- **AI Integration**: OpenRouter API integration for chatbot

## Installation

### Prerequisites
- Python 3.8 or higher
- pip (Python package manager)
- Virtual environment (recommended)

### Setup Steps

1. **Clone the repository**
```bash
git clone https://github.com/mukul1421/InventoryHub.git
cd InventoryHub
```

2. **Create a virtual environment**
```bash
python -m venv env
```

3. **Activate the virtual environment**

**Windows:**
```bash
env\Scripts\activate
```

**macOS/Linux:**
```bash
source env/bin/activate
```

4. **Install dependencies**
```bash
pip install -r requirements.txt
```

5. **Set up environment variables**

Create a `.env` file in the project root (copy from `.env.example`):
```bash
cp .env.example .env
```

Edit `.env` and add your configuration:
```
SECRET_KEY=your_secret_key_here
CHATBOT_API_KEY=your_openrouter_api_key
CHATBOT_API_URL=https://openrouter.ai/api/v1
DATABASE_URL=sqlite:///inventory.db
```

6. **Run the application**
```bash
python app.py
```

The application will be available at `http://localhost:5000`

## Default Credentials

The application creates default users on first run:

**Admin User:**
- Username: `admin`
- Email: `admin@example.com`
- Password: `admin123`

**Test User:**
- Username: `test_user`
- Email: `user@example.com`
- Password: `user123`

## Project Structure

```
InventoryHub/
├── app.py                 # Main Flask application
├── chatbot.py            # Chatbot integration and routes
├── seed_data.py          # Database seeding script
├── requirements.txt      # Python dependencies
├── .env.example          # Environment variables template
├── .gitignore           # Git ignore rules
├── static/
│   ├── css/
│   │   ├── index.css
│   │   ├── inventory.css
│   │   └── chatbot.css
│   ├── js/
│   │   ├── index.js
│   │   └── chatbot.js
│   └── images/
├── templates/
│   ├── base.html
│   ├── index.html
│   ├── login.html
│   ├── signup.html
│   ├── profile.html
│   ├── change_password.html
│   ├── dashboard.html
│   ├── admin_dashboard.html
│   ├── inventory.html
│   ├── item_form.html
│   ├── item_list.html
│   ├── group_form.html
│   ├── chatbot_ui.html
│   ├── about_us.html
│   ├── 404.html
│   ├── 500.html
│   ├── navbar.html
│   ├── sidebar.html
│   ├── footer.html
│   └── terms.html
├── instance/             # Flask instance folder
└── env/                  # Virtual environment (not committed)
```

## Database Models

### User
- id, username, email, password
- phone, country, state
- role (admin/user)
- last_login, created_at
- Relationships: items

### Item
- id, name, sku, type
- unit, quantity_in_hand, reorder_point
- cost_price, selling_price, tax_rate
- returnable flag
- user_id (foreign key)
- created_at, updated_at

### ItemGroup
- id, name, type
- description, unit
- returnable flag
- manufacturer, brand
- created_by, created_at

## API Routes

### Authentication
- `GET /` - Home page
- `POST /login` - User login
- `POST /register` - User registration
- `GET /logout` - User logout

### User Management
- `GET /profile` - View user profile
- `GET /change_password` - Change password form
- `POST /change_password` - Update password

### Inventory
- `GET /inventory` - Inventory overview
- `GET /items` - List all items
- `POST /item_form` - Add new item form
- `POST /item_form` - Create new item
- `POST /items/update/<id>` - Update item
- `POST /items/delete/<id>` - Delete item

### Item Groups
- `GET /groups` - List item groups
- `POST /groups` - Create new item group

### Dashboard
- `GET /dashboard` - User dashboard with analytics
- `GET /admin_dashboard` - Admin dashboard (admin only)
- `POST /admin/users/manage` - Manage users (admin only)

### Chatbot
- `GET /chatbot-ui` - Chatbot interface
- Chatbot endpoints via blueprint

## Usage Examples

### Creating an Item
1. Navigate to Inventory > Add Item
2. Fill in item details (name, SKU, unit, prices)
3. Set reorder point and tax rate
4. Click "Add Item"

### Tracking Stock
- View dashboard for real-time stock levels
- Get alerts for low stock items
- Monitor inventory value trends

### Admin Functions
- Manage users and assign roles
- View system-wide inventory statistics
- Monitor user activity and login history

## Troubleshooting

### Virtual Environment Issues
```bash
# Reactivate virtual environment
env\Scripts\activate  # Windows
source env/bin/activate  # macOS/Linux
```

### Database Errors
```bash
# Reset database (development only)
# Visit http://localhost:5000/reset_db
```

### Missing Dependencies
```bash
pip install -r requirements.txt --upgrade
```

## Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `SECRET_KEY` | Flask session secret key | ✅ |
| `CHATBOT_API_KEY` | OpenRouter API key for chatbot | ❌ |
| `CHATBOT_API_URL` | OpenRouter API endpoint | ❌ |
| `DATABASE_URL` | Database connection string | ❌ |

## Security Notes

⚠️ **Important:**
- Never commit `.env` file to version control
- Always use strong secret keys in production
- Change default admin credentials immediately in production
- Keep dependencies updated for security patches
- Use HTTPS in production
- Implement rate limiting for API routes
- Enable CSRF protection for all forms

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## Future Enhancements

- [ ] Advanced search and filtering
- [ ] Batch import/export (CSV, Excel)
- [ ] Production-ready deployment
- [ ] REST API with authentication tokens
- [ ] Email notifications for low stock
- [ ] Mobile app integration
- [ ] Enhanced reporting and analytics
- [ ] Multi-warehouse support
- [ ] Barcode scanning integration
- [ ] Integration with popular accounting software

## License

This project is open source and available under the MIT License.

## Support

For support, please open an issue in the GitHub repository or contact the development team.

## Authors

- **Mukul** - Initial development and maintenance

---

**Last Updated**: March 2026
**Version**: 1.0.0
