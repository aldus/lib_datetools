## lib_datetools

Modul (lib) for LEPTON-CMS that contains a simple (experimental) class  
for transform/modify dates in differ formats.

*This project is the follower of the [x_cDate] (https://github.com/aldus/x_cdate) class for WB/WBCE*

 
#### Author(-s)
- Dietrich Roland Pehlke (Aldus)

#### example

			//	new instance (via the internal autoloader)
			$oDateTool = lib_datetools::getInstance();

			//	setting the format
			$oDateTool->format="%A, %d. <font style='color:#900;'>%B</font> %Y";

			//	Use of the internal translation-array, e.g.
			if( isset( $oDateTool->CORE_date_formats[ DATE_FORMAT ] ))
			{
				$oDateTool->format = $oDateTool->CORE_date_formats[ DATE_FORMAT ];
			}

			// This will return the date-string in the given format.
			//	e.g. below: 11. März 1966
			echo $oDateTool->transform("11/03/1966");

			// 	This will return the current time in the format
			echo $oDateTool->toHTML();

			//	This also
			echo $oDateTool->toHTML( TIME() );

			//	This will set a new Language, e.g. italy
			$oDateTool->setLanguage( array ("it_IT", "italiy", "it_IT@euro") );

			//	This will change all dates in a given string (pass by reference!).
			$str = "At 30.03.1988 the new book of Mr. Unknown comes ... 12.2.1989 in Öttingen ";
			$oDateTool->parse_string( $str );
			echo $str;
			
			//	For the use in LEPTON-CMS/WBCE you can use the internal LANGUAGE or DEFAULT_LANGUAGE.
			//	Supported values at this time are: DE, EN, NL, IT, FR, RU, ZH
			$oDateTool->set_core_lang( LANGUAGE );

			//	This one will look for a languagekey inside all
			//	installed locales and then use them
			$result_list = $oDateTool->test_locale("de_AT", true);
			print_r( $result_list );
