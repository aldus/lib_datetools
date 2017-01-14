## lib_datetools

A simple (experimental) class for transform/modify dates in differ formats.

*This project is the follower of the x_cDate class for WB/WBCE*
 
#### Author(-s)
- Dietrich Roland Pehlke (aldus)

#### some example(-s)

			//	new instance (via the inernal autoloader)
			$oDateTool = lib_datetools::getInstance();

			//	setting the format
			$oDateTool->format="%A, %d. <font style='color:#900;'>%B</font> %Y";

			// This will return the date-string in the given format.
			//	e.g. below: 11. März 1966
			$oDateTool->transform ("11/03/1966");

			// 	This will return the current time in the format
			$oDateTool->toHTML();

			//	This also
			$oDateTool->toHTML ( TIME() );

			//	This will set a new Language, e.g. italy
			$oDateTool->setLanguage ( array ("it_IT", "italiy", "it_IT@euro") );

			//	This will change all dates in a given string (pass by reference!).
			$str = "At 30.03.1988 the new book of Mr. Unknown comes ... 12.2.1989 in Öttingen ";
			$oDateTool->parse_string ( $str );
			echo $str;
			
			//	For the use in LEPTON-CMS/WBCE you can use the internal LANGUAGE or DEFAULT_LANGUAGE.
			//	Supported values at this time are: DE, EN, NL, IT, FR, RU, ZH
			$oDateTool->set_core_lang ( LANGUAGE );

			//	This one will look for a languagekey inside all
			//	installed locales and then use them
			$oDateTool->test_locale("de_AT", true);

