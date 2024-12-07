# File_organiser
import os
import shutil

def organize_files(directory):
    # Check if the given directory exists
    if not os.path.isdir(directory):
        print(f"The directory '{directory}' does not exist. Please check the path and try again.")
        return  # Exit the function to prevent further errors

    # Get a list of files in the directory
    files = os.listdir(directory)

    if not files:
        print("The directory is empty. Nothing to organize.")
        return  # Exit if there are no files

    # Organize files based on extensions
    for file in files:
        file_path = os.path.join(directory, file)

        # Skip directories
        if os.path.isdir(file_path):
            continue

        # Get the file extension
        file_extension = file.split('.')[-1].lower() if '.' in file else 'others'
        folder_name = file_extension

        # Create a new folder for the extension if it doesn't exist
        folder_path = os.path.join(directory, folder_name)
        if not os.path.exists(folder_path):
            os.mkdir(folder_path)

        # Move the file to the appropriate folder
        shutil.move(file_path, os.path.join(folder_path, file))
        print(f"Moved {file} to {folder_name}/")

# Main function
def main():
    directory = input("Enter the path of the directory to organize: ").strip()
    organize_files(directory)

if __name__ == "__main__":
    main()
