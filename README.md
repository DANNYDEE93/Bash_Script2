# Bash_Script2

#!/bin/bash

# Provide menu to the user to select ssh or scp
# use case statement to provide commands for each choice

echo "Please choose (1 or 2):"
echo "1) ssh"
echo "2) scp"
read -p "Enter option to continue: " choice



case "$choice" in

#if ssh is chosen

   "1")
        echo "ssh selected"
        read -p "Enter IP_address: " IP
        read -p "Enter username: " User

#ssh into remote server with input credentials
#user must enter password when prompted

        ssh "$User@$IP"
        echo "Connected to remote server"

;;


# if user chooses scp
   "2")
        echo "scp selected"
        read -p "Enter remote IP address: " remoteIP
        read -p "Enter username: " remoteuser
        echo "1)remote -> local"
        echo "2)local ->remote"
        read -p "Enter option to continue: " option
        read -p "Enter path to source file location: " source_path
        read -p "Enter path to desitnation file location: " dest_path


#if user provides destinaition without file name, use basename to use filename from source_path

        destination=$(basename "$source_path")

#if user chooses remote to local

          if [ "$option" == 1 ]; then

                scp "$remoteuser@$remoteIP":"$source_path" "$dest_path"

          elif [ "$option" == 2 ]; then

                scp "$source_path" "$remoteuser@$remoteIP":"$dest_path"
          else:
                echo "Try again"
                fi

        echo "Transfer complete!"


;;

#needed to run case function
esac
