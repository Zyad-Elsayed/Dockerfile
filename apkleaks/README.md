1. build the image `sudo docker build -t apkleaks .`
2. edit your ~/.bash_profile or ~/.zsh_profile depending on the shell you are using
3. add
 ```
   apkleaks() {
    if [ $# -lt 1 ]; then
        echo "Usage: apkleaks <APK_FILE> [OPTIONS...]"
        echo "Options: [-o OUTPUT] [-p PATTERN] [-a ARGS] [--json]"
        return 1
    fi

    local apk_file="$1"
    shift

    # Copy the APK file to /tmp
    cp "$apk_file" /tmp/
    
    # Extract the filename
    local apk_filename=$(basename "$apk_file")
    
    # Run the Docker command
    sudo docker run -it --rm -v /tmp:/tmp apkleaks -f /tmp/"$apk_filename" "$@"

    # Remove the APK file from /tmp
    rm /tmp/"$apk_filename"
}
   ```
4. source ~/.bash_profile
5. you can use it now
   ![image](https://github.com/user-attachments/assets/32a15c02-ac57-4df5-855a-9d1b6ad9a075)


