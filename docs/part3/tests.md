# Tests

## Login Tests

1. correct username and password
2. correct username and wrong password
3. username does not exist
4. network failure  

## User/Role Management Tests
### Add User/Role
1. new user/role
2. username/rolename already in user/role table
3. network failure  

### Update User/Role
1. update username, password, roles /roleName,roleDescription,powers  
    check whether update succeed  
2. update a username/roleName already in user/role table  
3. network failure  

### Other Rules
1. Current user can't update his username and password  
	(this will cause user logout action normally)
2. One can not delete an administrator user account
3. One can not update/delete an administrator role information
4. Once be assigned an administrator role, one can not resign it