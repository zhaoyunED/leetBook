
C语言 关于几个字符串处理的函数，面试中会有问到的可能性
```
求字符串的长度
int strlen(const char* str)
{
	assert(NULL != str);
	int len;
	while( (*str ++) != '\0') len++;
	return len;
}

比较两个字符串
int strcmp(const char* str1,const char* str2)
{
	assert(NULL != str1 && NULL!=str2);
	int ret =0;
	while(!(ret = *(unsigned char*)str1 - *(unsigned char*)str2) && *str1)
	{
		str1++;
		str2++;
	}
	if(ret<0) return -1;
	else if(ret>0) return 1;
	
	return ret;
}

拼接字符串 将strSrc拼接到strDest
char *strcat(char *strDest,const char* strSrc)
{
	char *address = strDest;
	assert(NULL!=strDest && NULL != strSrc);
	while(*strDest) strDest++;
	while(*strDest++ = *strSrc++);
	return address;
}

字符串复制 将strSrc的内容复制到以strDest为起始位置的地方
char* strcpy(char* strDest,const char* strSrc )
{
	assert(NULL!=strDest && NULL != strSrc);
	char *strD = strDest;
	while( (*strDest++ = *strSrc++) !='\0' );
	return strD;
}
```