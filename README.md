Configuring the expense project using ansible roles:

- We have below playbooks.
    
    - db.yml
    
    - backend.yml
    
    - frontend.yml

- We have created the following roles structure:
    
    roles/
    
        db/
            tasks/
                main.yml	- Hold all the tasks related to db playbook.
            vars/
                main.yml	- Holds all the variables related to db playbook.
        
        backend/
            tasks/
                main.yml	- Hold all the tasks related to backend playbook.
            vars/
                main.yml	- Holds all the variables related to backend playbook.
            templates/
                backend.service.j2	- Holds the backend.service configuration. 
        
        frontend/
            tasks/
                main.yml	- Hold all the tasks related to frontend playbook.
            vars/
                main.yml	- Holds all the variables related to frontend playbook.
            templates/
                expense.conf.j2	- Holds the expense.conf configuration. 
            handlers/
                main.yml	- Holds the service restart tasks to make it only restart whenever it is required.
        
        common/
            tasks/
                app-pre-req.yml	- Holds all the tasks which are common across all the playbooks. And imported this role into the backend/tasks/main.yml file by using ansible.builtin.import_role:.
        
        main.yml	- Holds the common steps to call each playbook. With this we have to pass the component as an argument in the command.
                ansible-playbook main.yml -e component=db/backend/frontend
        
        credentials.yml	- It’s an ansible vault file which holds the sensitive data in encrypted format.
            - We have to run the playbook as below when we have ansible vault attached.
                ansible-playbook <playbook-name> --ask-vault-pass
