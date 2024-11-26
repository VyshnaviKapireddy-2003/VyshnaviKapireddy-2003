<!DOCTYPE html>

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Admin Dashboard</title>
    <style> 
      * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        } 
      body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            color: #333;
        }
      header {
            background-color: #4CAF50;
            color: white;
            text-align: center;
            padding: 20px;
        } 
      h1 {
            margin: 0;
            font-size: 2.5rem;
        }
      main {
            padding: 20px;
        }
      h2 {
            font-size: 1.8rem;
            margin-bottom: 20px;
            color: #333;
        }
      #user-management, #role-management {
            background-color: white;
            padding: 20px;
            margin-bottom: 30px;
            border-radius: 8px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }
      button {
            padding: 10px 20px;
            margin: 10px 0;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 1rem;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }
      button:hover {
            background-color: #45a049;
        }
      button:active {
            background-color: #388e3c;
        }
      table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }
      th, td {
            padding: 12px;
            text-align: left;
            border-bottom: 1px solid #ddd;
        }
      th {
            background-color: #4CAF50;
            color: white;
            font-size: 1.1rem;
        }
      td {
            font-size: 1rem;
            color: #555;
        }
      td button {
            padding: 5px 10px;
            background-color: #f0ad4e;
            border: none;
            border-radius: 5px;
            font-size: 0.9rem;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }
      td button:hover {
            background-color: #ec971f;
        }
      td button:active {
            background-color: #d58512;
        }
      #add-user-btn, #add-role-btn {
            background-color: #0275d8;
            font-size: 1rem;
        }
      #add-user-btn:hover, #add-role-btn:hover {
            background-color: #025aa5;
        }
      #add-user-btn:active, #add-role-btn:active {
            background-color: #014d8c;
        }
      @media (max-width: 768px) {
            table, th, td {
                font-size: 0.9rem;
            }
        button {
                font-size: 0.9rem;
            }
        }
    </style>
</head>
<body>
    <header>
        <h1>Admin Dashboard</h1>
    </header>
    <main>
        <section id="user-management">
            <h2>User Management</h2>
            <button id="add-user-btn">Add User</button>
            <table id="user-table">
                <thead>
                    <tr>
                        <th>ID</th>
                        <th>Name</th>
                        <th>Email</th>
                        <th>Role</th>
                        <th>Status</th>
                        <th>Actions</th>
                    </tr>
                </thead>
                <tbody id="user-table-body">
                    <!-- User rows will be dynamically inserted -->
                </tbody>
            </table>
        </section>
      <section id="role-management">
            <h2>Role Management</h2>
            <button id="add-role-btn">Add Role</button>
            <table id="role-table">
                <thead>
                    <tr>
                        <th>ID</th>
                        <th>Name</th>
                        <th>Permissions</th>
                        <th>Actions</th>
                    </tr>
                </thead>
                <tbody id="role-table-body">
                    <!-- Role rows will be dynamically inserted -->
                </tbody>
            </table>
        </section>
    </main>
    <script>
        document.addEventListener('DOMContentLoaded', function () {
            let users = [
                { id: 1, name: 'nikhila', email: 'nikhila@gmail.com', role: 'Admin', status: 'Active' },
                { id: 2, name: 'sony', email: 'sony@gmail.com', role: 'User', status: 'Inactive' }
            ];
          let roles = [
                { id: 1, name: 'Admin', permissions: ['Read', 'Write', 'Delete'] },
                { id: 2, name: 'User', permissions: ['Read'] }
            ];
           function renderUsers() {
                const userTableBody = document.getElementById('user-table-body');
                userTableBody.innerHTML = '';
                users.forEach(user => {
                    const row = document.createElement('tr');
                    row.innerHTML = `
                        <td>${user.id}</td>
                        <td>${user.name}</td>
                        <td>${user.email}</td>
                        <td>${user.role}</td>
                        <td>${user.status}</td>
                        <td>
                            <button onclick="editUser(${user.id})">Edit</button>
                            <button onclick="deleteUser(${user.id})">Delete</button>
                        </td>
                    `;
                    userTableBody.appendChild(row);
                });
            }
        function renderRoles() {
                const roleTableBody = document.getElementById('role-table-body');
                roleTableBody.innerHTML = '';
                roles.forEach(role => {
                    const row = document.createElement('tr');
                    row.innerHTML = `
                        <td>${role.id}</td>
                        <td>${role.name}</td>
                        <td>${role.permissions.join(', ')}</td>
                        <td>
                            <button onclick="editRole(${role.id})">Edit</button>
                            <button onclick="deleteRole(${role.id})">Delete</button>
                        </td>
                    `;
                    roleTableBody.appendChild(row);
                });
            }
            window.editUser = function (id) {
                const user = users.find(u => u.id === id);
                alert(`Editing user: ${user.name}`);
            }
            window.deleteUser = function (id) {
                users = users.filter(user => user.id !== id);
                renderUsers();
            }
         window.editRole = function (id) {
                const role = roles.find(r => r.id === id);
                alert(`Editing role: ${role.name}`);
          window.deleteRole = function (id) {
                roles = roles.filter(role => role.id !== id);
                renderRoles();
            }
 document.getElementById('add-user-btn').addEventListener('click', function () {
                const newUser = {
                    id: users.length + 1,
                    name: `New User ${users.length + 1}`,
                    email: `newuser${users.length + 1}@example.com`,
                    role: 'User',
                    status: 'Active'
                };
                users.push(newUser);
                renderUsers();
            });
 document.getElementById('add-role-btn').addEventListener('click', function () {
                const newRole = {
                    id: roles.length + 1,
                    name: `New Role ${roles.length + 1}`,
                    permissions: ['Read']
                };
                roles.push(newRole);
                renderRoles();
            });
           renderUsers();
            renderRoles();
        });
    </script>
</body>
</html>
