---
layout: post
title: "Read & Write file with multiple request"
date:   2015-03-24
description: Read & Write file with multiple request
categories: PHP
tags: php
---


These days, I got an issue. It was the file’s content would be emptied sometime. After checked code, we think the problem should happen when multiple request occur. Read and Write file were not in same lock. Actually we just add lock for write. So we change code as follow:

             $filename = APP_PATH . "filename";
             $fp = fopen($filename, 'c+');
             $vistor_count;
             if ($fp) {
                  flock($fp, LOCK_EX);
                  $vistor_count = intval(fread($fp, filesize($filename))) + 1;
                  //ftruncate($fp, 0);
                  rewind($fp);
                  fwrite($fp, strval($vistor_count));
                  fflush($fp);
                  flock($fp, LOCK_UN);
                  fclose($fp);
             }
