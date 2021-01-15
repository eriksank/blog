#About enforcing coding standards

I recenty read someone making the remark that he likes the CakePHP "coding standards". You can find these "coding standards" [here](http://book.cakephp.org/2.0/en/contributing/cakephp-coding-conventions.html) for version 2 of CakePHP. The first thing that crossed my mind was:

Hey, the regulation of language standards is itself a heavily regulated business and this person is not following the regulations.

The meta-regulations say that language regulations must be expressed as lexer and parser definitions. You can find the standard PHP lexer definition file [here](https://github.com/php/php-src/blob/master/Zend/zend_language_scanner.l). You can find the standard PHP LALR(1) parser definition file [here](https://github.com/php/php-src/blob/master/Zend/zend_language_parser.y).

It is definitely possible to extend these regulations and for example, insist that the PHP scripting engine refuses to execute programs that would otherwise be valid. However, this would have to be done in the format prescribed by the meta-regulations! You can find the meta-regulations [here](http://www.gnu.org/software/bison/manual/bison.html).

Where are the CakePHP coding standards that are themselves in accordance with the standards?

Both Flex (Lex) and Bison (Yacc) will reject invalid or simply unworkable programming language standards. What strikes me the most in these so-called "programming standards" is that the person writing them is usually unwilling or incapable of following the meta-rules. This is easy to check. This person's programming standards will never, ever compile correctly without yielding numerous error messages. Flex/Bison will keep refusing to deal with his failed attempts.

Such person will, however, often insist that other programmers follow their clearly invalid programming standards. How can a person who is incapable of following the rules insist that others would?

On the other hand, anybody I know who truly has the ability to specify such additional "programming standards", does not seem to be interested in doing so, if only because he usually has more interesting things to do.﻿

