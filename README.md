# CaesarCipher
Use this program to encode and decode words and sentences with a Caesar Cipher!

    #imports
    import simplegui

    #varriables
    user_word = ""										 #keeps track of the word the user enters
    shift = 0											 #keeps track of the amount that they want to shift the letters

    cipher_text = ""									 #keeps track of the ciphered text if they are encoding it
    ori_text = ""									 	 #keeps track of the decoded text if they are decoding it

    new_letter = ""									 	 #keeps track of the letters are they are shifted
    old_letter = ""									 	 #keeps track of the letters are they are shifted

    word_message1 = ""									 #tells the user their new encoded or decoded message
    word_message2 = ""									 #tells the user their new encoded or decoded message

    #helper functions
    def encode(text, key):						 		 #function that encodes sentence
        global cipher_text, new_letter, old_letter, word_message1, word_message2
        for char in user_word:							 #Loops through text
            if char == " ":								 #figures out if char is a space
                cipher_text = cipher_text + " " 		 #adds a space if char is space
            else:
                old_letter = ord(char) + shift			 #Change each letter to a number using ord and Shift each number
                new_letter = chr(old_letter)			 #Change the new number to a character using chr
                cipher_text = cipher_text + new_letter   #Add to cipher text
        print(cipher_text)
        word_message1 = ("Your encoded text is: " )
        word_message2 = cipher_text

    def decode(text, key):						 		 #function that decodes the cipher
        global ori_text, new_letter, old_letter, word_message1, word_message2
        for char in cipher_text:						 #Loops through text
            if char == " ":						 		 #figures out if char is a space
                ori_text = ori_text + " "  				 #adds a space if char is space
            else:
                old_letter = ord(char) - shift		     #Change each letter to a number using ord and Shift each number
                new_letter = chr(old_letter) 		     #Change the new number to a character using chr
                ori_text = ori_text + new_letter  		 #Add to cipher text
        print(ori_text)
        word_message1 = ("Your decoded text is: ")
        word_message2 = ori_text


    #event handlers
    def draw(canvas):									 #draw handler
        canvas.draw_text("Welcome to Caesar Cipher!", (75,75), 50, "black")
        canvas.draw_text("Enter your word, the shift amount, and click encode or decode.", (95,120), 20, "black")
        canvas.draw_text(word_message1, (95,200), 30, "black")
        canvas.draw_text(word_message2, (95,230), 30, "black")


    def input_word_handler(word_input):					 #event handler for the word input
        global user_word
        user_word = word_input
        print("user_word: ", user_word)

    def input_shift_handler(shift_input):				#event handler for the shift input
        global shift
        shift = int(shift_input)
        print("shift: ", shift)

    def button_encode_handler():						#event handler for the encode button
        encode(user_word, shift)						#calls the fucntion to encode

    def button_decode_handler():						#event handler for the decode button
        decode(user_word, shift)						#calls the function to decode

    #create the frame
    frame = simplegui.create_frame('Caesar Cipher', 700, 300)

    #set and create the handlers
    frame.set_canvas_background("pink")					 #sets the background color of the canvas
    frame.set_draw_handler(draw)						 #sets the draw handler
    frame.add_input("Word",input_word_handler,100)
    frame.add_input("Shift Amount",input_shift_handler,100)
    frame.add_button ("Encode", button_encode_handler)
    frame.add_button ("Decode", button_decode_handler)

    #start frame
    frame.start()
