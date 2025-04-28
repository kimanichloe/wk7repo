def modify_and_write_file(input_filename):
    """
    Reads a file, modifies each line (adds a timestamp), and writes the modified
    content to a new file. Handles potential file-related errors.
    """
    from datetime import datetime

    try:
        with open(input_filename, 'r') as infile:
            output_filename = f"modified_{input_filename}"
            try:
                with open(output_filename, 'w') as outfile:
                    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
                    for line in infile:
                        modified_line = f"[{timestamp}] {line.strip()}\n"
                        outfile.write(modified_line)
                print(f"Successfully processed '{input_filename}' and saved the modified version as '{output_filename}'.")
            except IOError:
                print(f"Error: Could not write to the file '{output_filename}'. Please check permissions.")
    except FileNotFoundError:
        print(f"Error: The input file '{input_filename}' was not found here in Kitengela. Please ensure the file exists.")
    except IOError:
        print(f"Error: Could not read the file '{input_filename}'. It might be corrupted or you may not have the necessary permissions.")

if __name__ == "__main__":
    while True:
        input_file = input("Enter the name of the file you want to process (or type 'exit' to quit): ")
        if input_file.lower() == 'exit':
            break
        modify_and_write_file(input_file)
