# cis6930sp24 -- Assignment1

## Name:
Sai Krishna Anugu
UFID: 42266064

## Assignment Description
In this assignment, we will design a data censoring system that accepts plain text documents and detects/censors sensitive information such as names, dates, phone numbers, and addresses. The system will be implemented in Python using libraries like spaCy and regular expressions.


## How to install
To set up the project environment, follow these steps:
1. Install Pipenv if you don't have it already.
2. Install project dependencies using Pipenv.


## How to run
pipenv run python censoror.py --input '*.txt' \
                    --names --dates --phones --address\
                    --output 'files/' \
                    --stats stderr

pipenv run python censoror.py --input 'input_texts/*.txt' --output 'censored_output/' --names --phones --dates --address --stats 'stats.txt'




# Functions: 
1. **censor_names(text)**
Purpose: This function is responsible for censoring names found in the given text.
Functionality:
It utilizes the spaCy library to perform named entity recognition (NER) on the input text.
For each named entity recognized as a person (labeled as "PERSON" by spaCy), it replaces the name with a sequence of black squares (█) of the same length, effectively censoring it.
The censored text with replaced names is then returned.
2.**censor_dates(text)**
Purpose: This function censors dates found in the given text.
Functionality:
It first utilizes spaCy to perform named entity recognition (NER) on the input text.
For each recognized date entity (labeled as "DATE" by spaCy), it replaces the date with a sequence of black squares (█) of the same length.
Additionally, it uses regular expressions to match various date formats not recognized by spaCy, such as MM/DD/YYYY, DD/MM/YYYY, month names, etc., and replaces them with black squares.
The censored text with replaced dates is then returned.
3. **censor_phones(text)**
Purpose: This function censors phone numbers found in the given text.
Functionality:
It utilizes regular expressions to match various phone number formats, including international prefixes, extensions, and common formats like (123) 456-7890, 123-456-7890, etc.
For each matched phone number, it replaces it with a sequence of black squares (█) of the same length.
The censored text with replaced phone numbers is then returned.
4. **censor_addresses(text)**
Purpose: This function censors addresses found in the given text.
Functionality:
It utilizes spaCy to perform named entity recognition (NER) on the input text.
For each recognized entity labeled as an organization (ORG), geopolitical entity (GPE), or location (LOC), it replaces the entity text with a sequence of black squares (█) of the same length.
Additionally, it uses enhanced regular expressions to match broader address patterns, including street names, numbers, and common abbreviations (e.g., Street, Ave, Rd, etc.).
The censored text with replaced addresses is then returned.
5. **main()**
Purpose: This function serves as the entry point of the module and provides an example of how to use the censoring functions individually.
Functionality:
It contains sample text with names, dates, phone numbers, and addresses.
It demonstrates how to apply each censoring function individually to the sample text and print the censored output.
Additionally, it showcases how to apply all censoring functions sequentially and print the fully censored output.




## Bugs
1. **Incorrect parsing of command-line arguments:** Errors may occur during command-line argument parsing if the user provides invalid or incomplete arguments. This bug could arise if the program does not properly handle edge cases or user mistakes, leading to unexpected behavior.

2. **Incorrect identification of sensitive information:** There may be cases where the censoring functions incorrectly identify sensitive information. For example, if a word that resembles a name or date is incorrectly labeled as such, it may be censored even though it is not sensitive information.


## Assumptions
1. Availability of spaCy models: The code assumes that the spaCy language model "en_core_web_md" is available for entity recognition. If this model is not installed or cannot be loaded, the program may raise an error.

2. Consistency in entity labeling: The code assumes that spaCy consistently labels names as "PERSON", dates as "DATE", organizations as "ORG", geographical locations as "GPE", and other locations as "LOC". Any inconsistencies in labeling by spaCy could lead to incorrect censorship.

3. Accuracy of regex patterns: The code relies on regular expressions to detect and censor sensitive information such as dates, phone numbers, and addresses. It assumes that these regex patterns accurately capture all variations of such information. Inaccurate or incomplete regex patterns may result in missed detections or incorrect censoring.





## Tests

## Test Case 1: test_censor_names
Description: This test case verifies if the censor_names function correctly censors names in the input text.

Input Text: "Hello, my name is John and I work with Jane."

Contains the name "John" and "Jane".
Expected Output: "Hello, my name is ████ and I work with ████."

The names "John" and "Jane" are replaced with a sequence of █ characters.


## Test Case 2: test_censor_dates
Description: This test case verifies if the censor_dates function correctly censors dates in the input text.

Input Text: "The meeting is scheduled for 12/25/2022 and the deadline is December 31, 2022."

Contains the date "12/25/2022" and the month "December 31, 2022".
Expected Output: "The meeting is scheduled for ██████████ and the deadline is █████████████████."

The dates are replaced with sequences of █ characters, maintaining the text structure.
These test cases ensure that the censoring functions censor_names and censor_dates accurately identify and censor the specified entities in the input text. If the functions work as expected, the output text should match the expected output provided in each test case.
