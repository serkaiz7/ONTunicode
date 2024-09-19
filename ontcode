import os

# Assuming you have cloned the Bible repository and the bible.txt is stored locally
BIBLE_FILE_PATH = "bible.txt"

# Function to load the Bible content into memory
def load_bible():
    with open(BIBLE_FILE_PATH, 'r', encoding='utf-8') as f:
        return f.read()

# Menu for selecting Old or New Testament
def select_testament():
    while True:
        print("\nSelect the Testament:")
        print("1. Old Testament")
        print("2. New Testament")
        choice = input("Enter 1 or 2: ")

        if choice == '1':
            return "old"
        elif choice == '2':
            return "new"
        else:
            print("Invalid choice, please try again.")

# Function for user to specify skip code and search parameters
def get_search_parameters():
    name_or_word = input("\nEnter the name or word to search: ")
    skip = int(input("Enter how many characters to skip: "))
    return name_or_word.lower(), skip

# Function to search for the name/word in the specified Testament using skip codes
def search_bible(content, search_word, skip):
    result_positions = []
    # Remove all newlines and spaces to create a continuous string
    cleaned_content = content.replace("\n", "").replace(" ", "").lower()
    content_length = len(cleaned_content)

    # Searching with the skip code
    for i in range(content_length):
        if cleaned_content[i] == search_word[0]:
            match = True
            for j in range(1, len(search_word)):
                if i + j * skip >= content_length or cleaned_content[i + j * skip] != search_word[j]:
                    match = False
                    break
            if match:
                result_positions.append(i)
    
    return result_positions

# Function to display surrounding events (verses) around the found positions
def get_events_around(content, positions, search_word):
    for pos in positions:
        # Extract surrounding events/verses
        start_pos = max(0, pos - 100)  # Start from 100 characters before
        end_pos = min(len(content), pos + 100)  # End at 100 characters after
        print("\nEvent around position {}:\n".format(pos))
        print(content[start_pos:end_pos])

# Main function to load the Bible, perform search, and display results
def main():
    # Load the Bible content
    if not os.path.exists(BIBLE_FILE_PATH):
        print("Bible file not found! Make sure you have the correct file path.")
        return
    
    bible_content = load_bible()

    # Select Testament
    testament = select_testament()

    # Separate Old and New Testament content
    old_testament, new_testament = bible_content.split("MATTHEW")  # Assuming split at start of New Testament

    if testament == "old":
        content = old_testament
    else:
        content = "MATTHEW" + new_testament  # Add the split marker back for New Testament

    # Get search parameters (word and skip code)
    search_word, skip = get_search_parameters()

    # Perform search using skip codes
    print("\nSearching for '{}' with a skip of {}...".format(search_word, skip))
    positions = search_bible(content, search_word, skip)

    if not positions:
        print("\nNo results found for '{}'.".format(search_word))
    else:
        print("\nFound '{}' at positions: {}".format(search_word, positions))
        get_events_around(content, positions, search_word)

if __name__ == "__main__":
    main()
