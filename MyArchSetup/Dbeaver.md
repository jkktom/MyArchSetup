# Installing and Using DBeaver on Arch Linux

DBeaver is a free, open-source universal database tool that supports various database systems including MySQL, PostgreSQL, SQLite, Oracle, and more.

## Action List

### 1. Install DBeaver

#### Option 1: Install from Official Repositories
```bash
# Update system packages
sudo pacman -Syu

# Install DBeaver Community Edition
sudo pacman -S dbeaver
```

#### Option 2: Install from AUR (if not available in official repos)
```bash
# Install git and base-devel if not already installed
sudo pacman -S git base-devel

# Clone the AUR package
git clone https://aur.archlinux.org/dbeaver.git
cd dbeaver

# Build and install the package
makepkg -si
```

#### Option 3: Install using Flatpak
```bash
# Install Flatpak if not already installed
sudo pacman -S flatpak

# Add Flathub repository
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

# Install DBeaver
flatpak install flathub io.dbeaver.DBeaverCommunity
```

### 2. Launch DBeaver

#### If installed from repositories or AUR
```bash
# Launch from terminal
dbeaver
```

#### If installed using Flatpak
```bash
flatpak run io.dbeaver.DBeaverCommunity
```

You can also find DBeaver in your application menu.

### 3. Connect to MySQL Database

1. Launch DBeaver
2. Click on "New Database Connection" (the plug icon)
3. Select "MySQL" from the list of database types
4. Enter the connection details:
   - Server Host: localhost
   - Port: 3306
   - Database: myapp_db (or the database name you specified)
   - Username: myapp_user (or the username you specified)
   - Password: Your password
5. Click "Test Connection" to verify the connection works
6. Click "Finish" to save the connection

### 4. Basic DBeaver Usage

#### Viewing Database Structure
- Expand your connection in the Database Navigator
- Browse through tables, views, and other database objects

#### Executing SQL Queries
1. Right-click on your connection and select "SQL Editor"
2. Write your SQL query in the editor
3. Press Ctrl+Enter or click the "Execute SQL Statement" button to run the query

#### Managing Data
- Right-click on a table and select "View Data" to see and edit table contents
- Use "Edit Value" to modify cell data
- Use "SQL Editor" for more complex operations

### 5. Troubleshooting

#### Connection Issues
- Verify MySQL container is running: `docker ps`
- Check port mapping: `docker port mysql-container`
- Ensure firewall allows connections to port 3306

#### Driver Issues
- Go to Help > Driver Manager
- Find MySQL driver and click "Edit"
- Click "Find Class" to locate the driver
- If needed, click "Download" to get the latest driver

### 6. Useful DBeaver Features

- **ER Diagrams**: Right-click on a schema and select "View Diagram"
- **Data Export/Import**: Right-click on a table and select "Export Data" or "Import Data"
- **SQL History**: View > SQL Manager > History
- **Execution Plans**: Enable "Explain Plan" in the SQL Editor

### 7. Keeping DBeaver Updated

```bash
# For official repository installation
sudo pacman -Syu

# For AUR installation
cd dbeaver
git pull
makepkg -si

# For Flatpak installation
flatpak update
```