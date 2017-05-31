## Service
Service is just a normal JavaScript (TypeScript) class. To create a service just create a `.ts` file with the `service` name.

myserv.service.ts
```javascript
export class LoggingService {
   logStatusChange(status: string) {
        console.log('A server status changed, new status: ' + status);
   }
}
```
Use dependency injection to provide an instance of this service to the component that uses a method from the service class:

app.component.ts
```javascript
import { Component, EventEmitter, Output } from '@angular/core';
import {LoggingService} from '../logging.service';  //import the file with the service
@Component({
  selector: 'app-new-account',
  templateUrl: './new-account.component.html',
  styleUrls: ['./new-account.component.css'],
  providers: [LoggingService]  // provide the service class
})
export class NewAccountComponent {
  @Output() accountAdded = new EventEmitter<{name: string, status: string}>();

  constructor(private loggingService: LoggingService) {}  // inject the service

  onCreateAccount(accountName: string, accountStatus: string) {
    this.accountAdded.emit({
      name: accountName,
      status: accountStatus
    });   
   this.loggingService.logStatusChange(accountStatus); // use a method from the service
  }
}
```
