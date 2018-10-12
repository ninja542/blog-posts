# Markdown file

Insert Notes about python
python is amazing

## header 2

* bullet points
* more bullet
* dfsalkjdfhasldkjf
* salkdjfsf

```python
alphabet = "abcdefghijklmnopqrstuvwxyz"
answer = input("Would you like to (D)ecrypt, (E)ncrypt or (Q)uit? ")
while (answer.upper() != "Q" and answer.upper() != "E" and answer.upper() != "D"):
	answer = input("Would you like to (D)ecrypt, (E)ncrypt or (Q)uit? ")
while answer.upper() != "Q":
	keyword_str = input("Please enter a keyword: ")
	while len(keyword_str) > 26 or keyword_str.isalpha() == False:
		print("There is an error in the keyword. It must be all letters and a maximum length of 26")
		keyword_str = input("Please enter a keyword: ")
		keyword_str = keyword_str.lower()
	message_str = input("Enter your message: ")
	message_str = message_str.lower()
	subkey = ""
	affinekey = alphabet
	for i in keyword_str + alphabet:
		if i not in subkey:
			subkey += i
	for i in alphabet:
		affinekey = affinekey[0:subkey.find(i)] + subkey[(subkey.find(i) * 5 + 8 ) % 26] + affinekey[subkey.find(i) + 1:]
	final_str = "" # final string to be displayed after doing the ciphers
	if (answer.upper() == "E"):
		for j in message_str:
			if j.isalpha():
				final_str += affinekey[alphabet.find(j)]
			else:
				final_str += j
		print("your encoded message:", final_str)
	elif (answer.upper() == "D"):
		for j in message_str:
			if j.isalpha():
				final_str += alphabet[affinekey.find(j)]
			else:
				final_str += j
		print("your decoded message:", final_str)
	answer = input("Would you like to (D)ecrypt, (E)ncrypt or (Q)uit? ")
print("See you again soon!")

```