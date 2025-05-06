### *March 13* 
Need better error handling on frontend, Use {"error_type":"ERR_LOGINCREDWRONG"} ,"ERR_REGISTERCHECKCRED,","ERR_LOGINTWOFACTORCODEMISSING" etcc.   doine
 Centralized logging if possible  
Then use switch or map errors, navigate based on errors instead of httpcodes. paritally done and working
Use same error types for everything.  done
Enable logging based on *Zap* Uber  -not done
Create Settings Dashboard. -not done
Logout token in JSON and verify if present there. --burn token -not done
Change Password in Settings -frontend
Setup 2FA in Settings -frontend

### *March 14*
Add message broker via NATS for compiler. 
Refactor the code to execute both compiler code and problem execution code. 
Build ProblemSolutionService in mongodb with frontend. 
