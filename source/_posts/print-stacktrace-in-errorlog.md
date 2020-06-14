---
layout: post
title: "Print Stack Trace in error log"
date:   2016-02-05
description: Print Stack Trace in error log
categories: PHP
tags: php
---

```
foreach ( debug_backtrace() as $key => $value ) {
	$function = @$value['function'];
	if( isset( $value['class'] ) )
		$function = $value['class'] . '::' . $function;
	//error_log( "** " . $key . ". " . $function . "( " . str_replace( array("\n","\t",' ','(',')'), '', print_r( $value['args'], true ) ) . " )" );
	//error_log( "** " . $key . ". " . $function . "( " . implode( ', ', @$value['args'] ) . " )" );
	error_log( "** " . $key . ". " . $function . "( " . serialize( @$value['args'] ) . " )" );
	error_log( "** FILE: " . @$value['file'] . ":" . @$value['line'] );
}
```