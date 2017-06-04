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

### Service for Data Storage
Hierarchical Injector - when you create a service, Angular knows how to create an instance of this service for this component and all its child components. They all will recieve the same instance of this service. The highest possible level is AppModule. If you porvide a service instance to the AppModule, the same service instance will be available to the whole app. The next is AppCompoent. The instanceds do not propagate up, only down.

To use the same instance of service do not include that service class in `providers`.
accounts.service.ts
```javascript
export class AccountsService {
      accounts = [
    {
      name: 'Master Account',
      status: 'active'
    },
    {
      name: 'Testaccount',
      status: 'inactive'
    },
    {
      name: 'Hidden Account',
      status: 'unknown'
    }
  ];

  addAccount(name: string, status: string) {
    this.accounts.push({name: name, status: status})
  }

  updateStatus(id: number, status: string) {
    this.accounts[id].status = status;
  }
}
```
app.components.ts
```javascript
import { Component } from '@angular/core';
import { AccountsService } from './accounts.service';
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css'],
  providers: [AccountsService]
})
export class AppComponent {

  accounts: {name: string, status: string}[] = [];

  constructor(private accountsService: AccountsService) {}
  
  ngOnInit() {
    this.accounts = this.accountsService.accounts;
  }
  
  onAccountAdded(newAccount: {name: string, status: string}) {
    this.accounts.push(newAccount);
  }

  onStatusChanged(updateInfo: {id: number, newStatus: string}) {
    this.accounts[updateInfo.id].status = updateInfo.newStatus;
  }
}
```
account.component.ts
```javascript
import { Component, Input } from '@angular/core';
import { LoggingService} from '../logging.service';
import { AccountsService } from '../accounts.service';

@Component({
  selector: 'app-account',
  templateUrl: './account.component.html',
  styleUrls: ['./account.component.css'],
  providers: [LoggingService]
})
export class AccountComponent {
  @Input() account: {name: string, status: string};
  @Input() id: number;
  
  constructor(private loggingService: LoggingService,
    private accountsService: AccountsService) {}

  onSetTo(status: string) {
    this.accountsService.updateStatus(this.id, status)
    this.loggingService.logStatusChange(status);
  }
}
```
new-account.components.ts
```javascript
import { Component } from '@angular/core';
import { LoggingService } from '../logging.service';
import { AccountsService } from '../accounts.service';

@Component({
  selector: 'app-new-account',
  templateUrl: './new-account.component.html',
  styleUrls: ['./new-account.component.css'],
  providers: [LoggingService]
})
export class NewAccountComponent {
 
  constructor(private loggingService: LoggingService,
    private accountsService: AccountsService) {}

  onCreateAccount(accountName: string, accountStatus: string) {
   this.accountsService.addAccount(accountName, accountStatus)
   this.loggingService.logStatusChange(accountStatus);
  }
}
```
