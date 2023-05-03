Download Link: https://assignmentchef.com/product/solved-cs0449-project-1-hangman-and-wav-files
<br>
<h1></h1>

Hangman is a word-guessing game. In Hangman, a word is chosen. You are shown a sequence of blanks, one for each character, so you know how long the word is. You must guess the word by guessing which letters are in it.

Every time you guess a letter <strong>correctly,</strong> all copies of that letter are revealed. If you guess all the letters, <em>or</em> if you guess the word, you win.

Every time you guess a letter or the word <strong>incorrectly,</strong> you get a strike. When you get <strong>five strikes,</strong> the game is over and you lose.

Here is a sample game of the player guessing the word “apple” successfully:

$ ./hangmanWelcome to hangman! Your word has 5 letters:_ _ _ _ _ Guess a letter or type the whole word: sStrike 1!_ _ _ _ _ Guess a letter or type the whole word: e_ _ _ _ e Guess a letter or type the whole word: aa _ _ _ e Guess a letter or type the whole word: pa p p _ e Guess a letter or type the whole word: appieStrike 2!a p p _ e Guess a letter or type the whole word: appleYou got it! The word was ‘apple’.

Notice when they guessed ‘p’, it showed <em>all</em> the <strong>p</strong>’s in the word.

And here they are failing to guess the word “apple”:

$ ./hangmanWelcome to hangman! Your word has 5 letters:_ _ _ _ _ Guess a letter or type the whole word: sStrike 1!_ _ _ _ _ Guess a letter or type the whole word: afterStrike 2!_ _ _ _ _ Guess a letter or type the whole word: xStrike 3!_ _ _ _ _ Guess a letter or type the whole word: qStrike 4!_ _ _ _ _ Guess a letter or type the whole word: sStrike 5!Sorry, you lost! The word was ‘apple’.

Notice they guessed the letter ‘s’ twice. You <strong>don’t</strong> have to remember “wrong” letters. They can just look at their previous guesses &#x1f61c;

Last, to help with testing and grading, your program should accept one command-line argument as the word to guess:

$ ./hangman scrumbusWelcome to hangman! Your word has 8 letters:_ _ _ _ _ _ _ _ Guess a letter or type the whole word: ss _ _ _ _ _ _ s Guess a letter or type the whole word: us _ _ u _ _ u s Guess a letter or type the whole word: scrumbusYou got it! The word was ‘scrumbus’.

That way, you can run it with a known word and see if it behaves the way you expect.

<h2>The Dictionary</h2>

I am providing you with a <strong>text file</strong> containing a dictionary of words to use. <a href="/teaching/classes/cs0449/projects/dictionary.txt">Here it is.</a> Right-click and save the link. You’ll have to upload it to your AFS space with your SFTP client.

If you open this file, you will see a number on the first line, and then a bunch of words.

The <strong>first line</strong> says how many words there are in the dictionary. Then, each line after that is one word.

So, to read the dictionary:

<ol>

 <li>Read the first line with fgets and use atoi (from stdlib.h) or sscanf (from stdio.h) to parse the number out of it.</li>

 <li>Create an <strong>array of strings</strong> with that length.

  <ul>

   <li>You can use the syntax char words[length][20] to make the array.</li>

   <li>This will limit each word to 19 characters, but none of the words are nearly that long.</li>

  </ul></li>

 <li>Read each subsequent line of the file into the array.

  <ul>

   <li>You can use words[i] and sizeof(words[i]) the way you’re used to.</li>

  </ul></li>

</ol>

<h3>Tips:</h3>

<ul>

 <li><strong>Remember to check if </strong><strong>fopen</strong><strong> returned </strong><strong>NULL</strong><strong>!</strong>

  <ul>

   <li>If so, you can return from main or use exit from stdlib.h to exit the program.</li>

  </ul></li>

 <li><strong>Feel free to use any example code I have given you.</strong>

  <ul>

   <li>Things like get_line, streq_nocase etc will be helpful.</li>

   <li>You’ll probably want to make a version of get_line to read from an arbitrary FILE* instead of only stdin.</li>

  </ul></li>

 <li><strong>Test your code before you make the game.</strong>

  <ul>

   <li>Print out the dictionary after reading it into the array.</li>

   <li>If you’re getting blank lines between words, you probably didn’t chop the 
 off the lines when you read them.</li>

  </ul></li>

</ul>

<h2>The game</h2>

<strong>Once you’re sure you’re reading the dictionary in properly,</strong> you can move onto the game.

It works like this:

<ol>

 <li>Pick a random word from the dictionary (see below).

  <ul>

   <li>Alternatively, if argc &gt; 1, use argv[1] as the word instead.</li>

  </ul></li>

 <li>Tell the player how many letters there are in the word.</li>

 <li>In a loop:</li>

</ol>

<ol>

 <li style="list-style-type: none;">

  <ol>

   <li>Show the current state of the word (see the interactions above to see how to print it out).</li>

   <li>Ask the user for a letter or word.</li>

   <li>If they didn’t type anything, go back to the previous step and ask them again.</li>

   <li>If they typed a single letter,

    <ul>

     <li>If it’s in the word at least once, mark all instances of that letter as “revealed”.

      <ul>

       <li>If all the letters are revealed, <strong>they win, and the program is over.</strong></li>

      </ul></li>

     <li>If it’s not in the word, they get a strike. Show how many strikes they have.</li>

    </ul></li>

   <li>If they typed a word (more than 1 letter),

    <ul>

     <li>If it’s correct (equal to the word you picked), <strong>they win, and the program is over.</strong></li>

     <li>If it’s not correct, they get a strike. Show how many strikes they have.</li>

    </ul></li>

   <li>If they have 5 strikes, <strong>they lose, and the program is over.</strong>

    <ul>

     <li>Show them the correct word.</li>

    </ul></li>

  </ol></li>

</ol>

Notes:

<ul>

 <li>If they guess a letter they have guessed before, <strong>don’t handle it specially.</strong>

  <ul>

   <li>If they guess a correct letter twice, nothing bad will happen.</li>

   <li>If they guess an incorrect letter twice, that’s the user’s fault &#x1f61c;</li>

  </ul></li>

 <li><strong>Try to split things into functions.</strong></li>

 <li><strong>Do not add extra prompts/questions, and do not be too picky about user input.</strong>

  <ul>

   <li>Accept lower- AND upper-case letters for their guesses, using streq_nocase from lab2.</li>

   <li>User experience is an important part of program design!

    <ul>

     <li>And it will make it faster and easier to grade your projects &#x1f609;</li>

    </ul></li>

  </ul></li>

</ul>

<h3>Random numbers</h3>

To generate random numbers:

<ul>

 <li>#include &lt;stdlib.h&gt; and #include &lt;time.h&gt;</li>

</ul>

<ul>

 <li><strong>ONCE</strong> at the beginning of the program, “seed” the random number generator like so:</li>

</ul>

·           srand((unsigned int)time(NULL));

This method will generate slightly biased results and should not be used to generate a range of random numbers in general. For something this simple, it’s fine.

<ul>

 <li>When you need an <strong>exclusive</strong> range of random numbers such as [0, 2) do this:</li>

</ul>

·           rand() % (high_value – low_value) + low_value

<ul>

 <li><strong>Write a function</strong> to do this. random_range(1, 10) makes more sense and is more readable than rand() % 9 + 1.</li>

</ul>

<h1>[65%] wavedit.c</h1>

Now you’ll write a program to read and do simple operations on a common sound file format called WAV.

The way we record sound is by recording how the air pressure changes over time. In digital sound, we take thousands of measurements (“samples”) each second, and store each measurement as a number.

Here’s a diagram of a simple sound wave, represented by the red line; and the digital version of it, represented by the individual blue dots. Each dot is one sample, and each sample can be one of 16 different values.

<em>Thanks, Wikipedia. Thikipedia.</em>

<h2>The WAV file format</h2>

If you’re curious, chunk-based file formats are very common and pretty simple and flexible. <a href="https://docs.python.org/3.7/library/chunk.html">Python even has a library for them.</a> Cause, like, of course it does.

WAV files use a binary file format called RIFF, which is a “chunk-based” file format. However, the file format is simple enough that we can kind of treat it as a fixed format.

<strong>At the very beginning of the file,</strong> this structure appears (offsets and sizes are measured in bytes). What these fields should contain is explained a little further down.

<table>

 <thead>

  <tr>

   <td><strong>Offset</strong></td>

   <td><strong>Size</strong></td>

   <td><strong>Name</strong></td>

   <td><strong>Description</strong></td>

  </tr>

 </thead>

 <tbody>

  <tr>

   <td>0</td>

   <td>4</td>

   <td>riff_id</td>

   <td><em>chunk ID</em></td>

  </tr>

  <tr>

   <td>4</td>

   <td>4</td>

   <td>file_size</td>

   <td>size of rest of file, in bytes</td>

  </tr>

  <tr>

   <td>8</td>

   <td>4</td>

   <td>wave_id</td>

   <td><em>WAV file ID</em></td>

  </tr>

  <tr>

   <td>12</td>

   <td>4</td>

   <td>fmt_id</td>

   <td><em>chunk ID</em></td>

  </tr>

  <tr>

   <td>16</td>

   <td>4</td>

   <td>fmt_size</td>

   <td>size of the format info, in bytes</td>

  </tr>

  <tr>

   <td>20</td>

   <td>2</td>

   <td>data_format</td>

   <td>how the data is encoded</td>

  </tr>

  <tr>

   <td>22</td>

   <td>2</td>

   <td>number_of_channels</td>

   <td>how many channels (mono, stereo, surround etc)</td>

  </tr>

  <tr>

   <td>24</td>

   <td>4</td>

   <td>samples_per_second</td>

   <td>how many times per second the pressure was measured</td>

  </tr>

  <tr>

   <td>28</td>

   <td>4</td>

   <td>bytes_per_second</td>

   <td>how many bytes per second of sound</td>

  </tr>

  <tr>

   <td>32</td>

   <td>2</td>

   <td>block_alignment</td>

   <td>how many bytes per sample of all channels</td>

  </tr>

  <tr>

   <td>34</td>

   <td>2</td>

   <td>bits_per_sample</td>

   <td>how many bits each pressure measurement is</td>

  </tr>

  <tr>

   <td>36</td>

   <td>4</td>

   <td>data_id</td>

   <td><em>chunk ID</em></td>

  </tr>

  <tr>

   <td>40</td>

   <td>4</td>

   <td>data_size</td>

   <td>size of the sound data, in bytes</td>

  </tr>

 </tbody>

</table>

You must <strong>make a struct</strong> to represent this file header. (You could name it WAVHeader or something.)

When converting this table to a struct, keep these things in mind when deciding what types to use:

<ul>

 <li>The four _id members are char arrays.

  <ul>

   <li>Look at the size to see how long they should be.</li>

  </ul></li>

 <li>All the other members are <strong>unsigned integers.</strong>

  <ul>

   <li>The size will decide which type they should be.</li>

   <li>Look back at your exploration from lab 2 to see which types are which size.</li>

  </ul></li>

 <li>This whole struct should be <strong>44 bytes.</strong>

  <ul>

   <li>You can print sizeof(WAVHeader) or whatever you’ve named it to check.</li>

  </ul></li>

 <li>If you like, there is a header file called stdint.h which contains shorter, more precise type names for integers.

  <ul>

   <li>uint8_t, uint16_t, uint32_t, and uint64_t are unsigned 8-, 16-, 32-, and 64-bit integer types.</li>

   <li>You use them like any other type, e.g. uint8_t x; makes an unsigned 8-bit integer variable x.</li>

  </ul></li>

</ul>

<h2>Your program</h2>

OK, enough talk, let’s program!

You will make a utility that can:

<ul>

 <li>Check if a file really is a WAV file</li>

 <li>If it is, read and display useful information about it</li>

 <li>Change its speed</li>

 <li>Reverse the sound</li>

</ul>

Your program will work as a command-line program taking command-line arguments – <strong>NOT</strong> asking for input with fgets!

You will be able to run it four different ways:

./wavedit./wavedit somefile.wav./wavedit somefile.wav -rate 22050./wavedit somefile.wav -reverse

<h2>No arguments: ./wavedit</h2>

When run like this, your program should show a help message telling how to use it.

Try running cat –help on thoth to see what this kind of help or “usage” information usually looks like. Then make yours look kind of similar. &#x1f642;

<h2>One argument: ./wavedit FILENAME</h2>

When run like this, the first argument (argv[1]) will be the name of a file.

This should:

<ol>

 <li>Check that the file exists (by using fopen)

  <ul>

   <li>Which mode should you use to <strong>read</strong> a <strong>binary file?</strong></li>

  </ul></li>

 <li>Check that it really is a WAV file (see below)</li>

 <li>Display the format information and some other information. (see below)</li>

 <li>Don’t forget to close the file.</li>

</ol>

<strong>Make a function for each of these steps.</strong> Then it’ll be easy to reuse them for the other modes.

<h3>Checking that a file really is a WAV file</h3>

Remember from class that a file extension is just part of its name, and doesn’t mean that the file really is what it says it is. So, you must check the data in the file to ensure that it’s valid.

<strong>If any of these checks fail,</strong> display a message saying it’s an invalid WAV file and exit. Here’s how to check:

<ol>

 <li>Make a variable of your WAVHeader struct.</li>

 <li>Use <strong>a single </strong><strong>fread</strong><strong> call</strong> to read the struct from the file.</li>

 <li>Ensure that these fields have these values:

  <ul>

   <li>riff_id should contain the characters “RIFF”</li>

   <li>wave_id should contain the characters “WAVE”</li>

   <li>fmt_id should contain the characters “fmt ” (<strong>NOTE: there is a space in there!</strong>)</li>

   <li>data_id should contain the characters “data”</li>

   <li>fmt_size should be <strong>16</strong></li>

   <li>data_format should be <strong>1</strong></li>

   <li>number_of_channels should be <strong>1 or 2</strong></li>

   <li>samples_per_second should be <strong>greater than 0 and less than or equal to 192000</strong></li>

   <li>bits_per_sample should be <strong>8 or 16</strong></li>

   <li>bytes_per_second should be samples_per_second * (bits_per_sample)/8 * number_of_channels</li>

   <li>block_alignment should be (bits_per_sample)/8 * number_of_channels</li>

  </ul></li>

</ol>

<strong>To check the four </strong><strong>_id</strong><strong> fields,</strong> you <strong>CANNOT</strong> use strcmp/streq, because these are <em>not</em> C-style strings. They have no 0 terminator. Instead, use strncmp. Look it up!

<h3>Displaying the information</h3>

You should display the following information:

<ul>

 <li>The number of bits per sample</li>

 <li>The sample rate (samples per second), as Hz</li>

 <li>Whether it is mono (1 channel) or stereo (2 channels)</li>

 <li>The length of the data in <strong>samples</strong> (data_size / block_alignment)</li>

 <li>The length of the data in <strong>seconds</strong> (length in <strong>samples</strong>, divided by samples_per_second)

  <ul>

   <li>You’re gonna get a fraction here, so you <strong>must cast one of the values to a </strong><strong>float</strong><strong>!</strong></li>

   <li>Display this value with <strong>3 digits</strong> after the decimal point.</li>

  </ul></li>

</ul>

As an example, here is what my program outputs on the sine440_16.wav test file:

This is a 16-bit 44100Hz mono sound.It is 99225 samples (2.250 seconds) long.

<h2>Setting the sound’s sample rate: ./wavedit somefile.wav -rate 22050</h2>

This will <strong>change</strong> the file, by setting its samples_per_second field to the given number. It should:

<ol>

 <li>Parse the argument after the -rate argument, and ensure that it is <strong>greater than 0 and less than or equal to 192000.</strong>

  <ul>

   <li>Give an error and exit if not.</li>

  </ul></li>

 <li>Open the file and read the header

  <ul>

   <li>You’ll have to open it for <strong>reading AND writing</strong></li>

  </ul></li>

 <li>Check that it really is a WAV file, like before</li>

 <li>Set the samples_per_second in the struct to the rate given on the command line.</li>

 <li>Set the bytes_per_second in the struct to a new value calculated as:

  <ul>

   <li>samples_per_second * (bits_per_sample)/8 * number_of_channels</li>

  </ul></li>

 <li>Seek back to the <strong>beginning of the file</strong></li>

 <li>fwrite the struct back out to the file</li>

 <li>Don’t forget to close the file!</li>

</ol>

<h3>Did I do it right?</h3>

If you set the rate too high, your computer might refuse to play it. If so, try to stay at 48000 Hz and below.

Now, if you read the file’s properties again, everything should be the same, except the rate should have changed. If it says that the header is invalid, maybe you forgot to update the bytes_per_second value in the header.

Also, you can download the file with your SFTP client, and play it, and it should sound faster or slower &#x1f642;

Warning: iTunes likes to do stupid shit and will make copies of your files when you open them, and you’ll think your program isn’t working, when it is. This happened to me. Either delete the files from iTunes after listening, or use a different media player (VLC?).

<h2>Reversing a sound: ./wavedit somefile.wav -reverse</h2>

This will <strong>change</strong> the file, by reading all the samples, reversing them, and then writing them all back out again. It should work on 8- or 16-bit, mono or stereo sounds.

Here’s what it should do

<ol>

 <li>Open the file and read the header

  <ul>

   <li>You’ll have to open it for <strong>reading AND writing</strong></li>

  </ul></li>

 <li>Check that it really is a WAV file, like before</li>

 <li>Calculate the <strong>data length in samples,</strong> like before</li>

 <li>Allocate an array of the right type and that length (see below)</li>

 <li><strong>Use a single </strong><strong>fread</strong><strong> call</strong> to read the whole array from the file

  <ul>

   <li>After you read the header, the file is already in the right place to read the data</li>

  </ul></li>

 <li>Reverse the array’s values

  <ul>

   <li>That is, swap the first and last values; then the second and second-to-last; etc.</li>

  </ul></li>

 <li>Seek back to the beginning of the file plus sizeof(WAVHeader)</li>

 <li><strong>Use a single </strong><strong>fwrite</strong><strong> call</strong> to write the whole array back to the file</li>

 <li>Don’t forget to close the file!</li>

</ol>

<h3>How samples are stored</h3>

For <strong>mono</strong> (1-channel) sounds, the samples are simply an array. If bits_per_sample is 8, it’s an array of 8-bit integers. If it’s 16, it’s an array of 16-bit integers.

For <strong>stereo</strong> (2-channel) sounds, each sample is stored as a <strong>pair</strong> of 8- or 16-bit integers. The first number in the pair is the left channel’s sample, and the second number is the right channel’s.

Since your reversing function doesn’t have to treat the stereo channels individually, you can treat the data array as follows:

<ul>

 <li>If bits_per_sample is 8 and number_of_channels is 1:

  <ul>

   <li>treat it as an array of <strong>8-bit integers.</strong></li>

  </ul></li>

 <li>If bits_per_sample is 16 and number_of_channels is 1; OR</li>

 <li>If bits_per_sample is 8 and number_of_channels is 2:

  <ul>

   <li>treat it as an array of <strong>16-bit integers.</strong></li>

  </ul></li>

 <li>If bits_per_sample is 16 and number_of_channels is 2:

  <ul>

   <li>treat it as an array of <strong>32-bit integers.</strong></li>

  </ul></li>

</ul>

Since C doesn’t have generics or function overloading, you’ll have to repeat this code three times, but with different types. Sorry ¯_(ツ)_/¯

You can allocate the arrays like in hangman: sometype samples[sample_length]; where sometype is one of the types listed above.

When you fread, you <em>can</em> actually use sizeof() on that array, and it <em>will</em> give you the correct size of the array in bytes. At runtime. I know. <em>I kind of lied.</em> &#x1f609;

<h3>Did I reverse it correctly?</h3>

The best way to check is to use your ears. Use the stereo_ and speech_ test files given below. After you run your program, download it in your SFTP client and listen to it.

<h2>Test files</h2>

Here are some test WAV files to use, <strong>but your program will be graded with others.</strong> You can copy them to your directory like so:

cp ~jfb42/public/cs449/*.wav .

Don’t forget the space and period in the above command.

If you mess up or corrupt the files somehow, don’t worry, just run this command again to get clean copies of them.

The files should have the following properties by default:

<ul>

 <li>sine440_16.wav: 16-bit, 44100Hz, mono, 99225 samples, 2.250 seconds</li>

 <li>sine440_8.wav: 8-bit, 44100Hz, mono, 99225 samples, 2.250 seconds</li>

 <li>speech_16.wav: 16-bit, 44100Hz, mono, 103936 samples, 2.357 seconds</li>

 <li>speech_8.wav: 8-bit, 44100Hz, mono, 103936 samples, 2.357 seconds</li>

 <li>stereo_16.wav: 16-bit, 44100Hz, stereo, 112128 samples, 2.543 seconds</li>

 <li>stereo_8.wav: 8-bit, 44100Hz, stereo, 112128 samples, 2.543 seconds</li>

 <li>woosh_16.wav: 16-bit, 44100Hz, stereo, 220500 samples, 5.000 seconds</li>

 <li>woosh_8.wav: 8-bit, 44100Hz, stereo, 220500 samples, 5.000 seconds</li>

</ul>