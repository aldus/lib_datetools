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

		// 1.2	not all dates
		$sTestText = "<br /><br /><b>The</b> date 23.4.18 will be converted, the #!23.4.19 will not and the 15.5.15 will be.";
		$oDateTool->parse_string( $sTestText, "/[^#][^!]([0-3][0-9].[01]{0,1}[0-9].[0-9]{2,4})/s"  );
		echo str_replace("#!", "", $sTestText);

		// 1.3	Mixed dates
		$sTestText = "<br /><br />Some mixed dates: 23.4.18 will be converted, the #!23.4.19 will be another language and the 15.5.15 will be converted into the first one.";
		$oDateTool->parse_string( $sTestText, "/[^#][^!]([0-3][0-9].[01]{0,1}[0-9].[0-9]{2,4})/s"  );

		//	1.3.1 Set up another language and format 
		$oDateTool->set_core_language( "FR" );
		$oDateTool->format="<strong>%A, %d. <font style='color:#909;'>%B</font> %Y</strong>";
		$oDateTool->parse_string( $sTestText, "/[#][!]([0-3][0-9].[01]{0,1}[0-9].[0-9]{2,4})/s"  );

		//	1.3.2	Output the result
		print str_replace("#!", "", $sTestText);
