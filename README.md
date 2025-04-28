# mygrep.sh
#!/bin/bash

# Usage function
usage() {
    echo "Usage: $0 [-n] [-v] search_string filename"
    exit 1
}

# Check arguments
[ $# -lt 2 ] && usage

# Parse options
while [[ "$1" == -* ]]; do
    case "$1" in
        -n) show_line_numbers=true; shift ;;
        -v) invert_match=true; shift ;;
        --help) usage ;;
        *) echo "Invalid option: $1"; usage ;;
    esac
done

# Get remaining arguments
search_string="$1"
file="$2"

# Validate arguments
[ -z "$search_string" ] || [ -z "$file" ] && usage
[ -f "$file" ] || { echo "Error: File '$file' not found."; exit 1; }

# Search with grep
grep_command="grep -i"
[ "$show_line_numbers" = true ] && grep_command="$grep_command -n"
[ "$invert_match" = true ] && grep_command="$grep_command -v"
$grep_command "$search_string" "$file"
![image](https://github.com/user-attachments/assets/31cdcf32-2fca-44f6-8b6b-ed3963d06a25)
![image](https://github.com/user-attachments/assets/5eab3102-a94e-4391-8572-118bab949308)
![image](https://github.com/user-attachments/assets/7e64f02a-3112-4d46-8565-e65a652d2244)


