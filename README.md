This is for production installation of Galaxy using ansible on Ubuntu servere 18.04
- Do not install ansible from default repo as it will install version 2.5 which will not work. Required ansible version is >=2.7. Install it using 
    - sudo apt-add-repository ppa:ansible/ansible
    - sudo apt install ansible # it will install version 2.9.x
- User used for installation should have passwordless sudo access.
- Installation will complete but Ngnix will show balnk page beacuse of permission issue. Add user www-data to group galaxy.

    usermod -aG galaxy www-data
- restart Nginx "sudo systmectl restart nginx"
- Tool installation may not work beacuse of permission issue for user galaxy on dir /srv/galaxy. Correct permissions "chown -R galaxy:galaxy /srv/galaxy this may need to run with every change or else edit /home/osb/galaxy/roles/galaxyproject.galaxy/tasks/paths.yml for permissions 750 > 770 for "__galaxy_dir_perms: "{{ '0770' if __galaxy_user_group == __galaxy_privsep_user_group else '0755' }}""
-

