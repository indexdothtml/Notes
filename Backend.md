# Backend notes

## Rules
1. Never use 'g' or 'global' flag in regex expression while validating email or password using regex.
2. Sending request with 'form-data' requires middleware that can handle 'multipart/form-data' like 'multer' package. 'form-data' request can handle files, which requires special package ex- multer.
3. Sending only text data, then just sending request with 'raw json' is fine.
4. Unused parameters in controllers or middlewares functions such as 'req, res, err, next' can be replaced with _ (underscore), suppose if 'req' is not used then it can be written like this (_, res, err, next)   
