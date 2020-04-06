---
layout: post
title: Ionic Debounce
category: 前端
tags: [ionic , Debounce]
description: Ionic Debounce
---
  

原文地址 [https://stackoverflow.com/questions/32051273/angular-and-debounce](https://stackoverflow.com/questions/32051273/angular-and-debounce)
  [https://github.com/judgewest2000/IonicInputDebounceExample](https://github.com/judgewest2000/IonicInputDebounceExample)


html
 ```html
<ion-header>
  <ion-navbar>
    <ion-title>
      Search
    </ion-title>
  </ion-navbar>
</ion-header>

<ion-content >

  <ion-list>
    <ion-item>
      <ion-input type="text" placeholder="Enter your search in this input field..." [formControl]="textInput"></ion-input>
    </ion-item>
  </ion-list>


  <ion-list>
    <ion-item *ngFor="let item of filteredItems">
      {{item}}
    </ion-item>
  </ion-list>
</ion-content>
 ```

Component
 ```
import { NavController } from 'ionic-angular';

import { Component } from '@angular/core';
import { FormControl } from '@angular/forms';
import 'rxjs/add/operator/debounceTime';

@Component({
  selector: 'page-home',
  templateUrl: 'home.html'
})
export class HomePage {

  user:any;

  textInput = new FormControl('');

  listItems = ['pepsi', 'coke', 'dr pepper', '7up', 'mountain dew', 'sprite'];

  currentSearchValue = '';

  get filteredItems() {
    return this.listItems.filter(li => this.stringTools.contains(li, this.currentSearchValue));
  }

  stringTools = {
    contains: (source: string, lookupValue: string) => {
      if (source === undefined || source === null) {
        return false;
      }

      return source.toLowerCase().indexOf(lookupValue.toLowerCase()) !== -1;
    }
  }



  constructor(public navCtrl: NavController) {

    this.textInput
      .valueChanges
      .debounceTime(500)
      .subscribe(value => this.currentSearchValue = value);

  }
}
 ``` 
 
## DebounceDirective 
 
 ts
 ```
 import { Directive, Input, Output, EventEmitter,ElementRef } from '@angular/core';
import { NgControl, NgModel } from '@angular/forms';
import 'rxjs/add/operator/debounceTime'; 
import 'rxjs/add/operator/distinctUntilChanged';
import { Observable } from 'rxjs/Observable';
import 'rxjs/add/observable/fromEvent';
import 'rxjs/add/operator/map';

@Directive({
    selector: '[ngModel][debounce]',
})
export class DebounceDirective {
    @Output()
    public onDebounce = new EventEmitter<any>();

    @Input('debounce')
    public debounceTime: number = 500;

    private isFirstChange: boolean = true;

    constructor(private elementRef: ElementRef, private model: NgModel) {
    }

    ngOnInit() {
        const eventStream = Observable.fromEvent(this.elementRef.nativeElement, 'keyup')
            .map(() => {
                return this.model.value;
            })
            .debounceTime(this.debounceTime);

        this.model.viewToModelUpdate = () => {};

        eventStream.subscribe(input => {
            this.model.viewModel = input;
            this.model.update.emit(input);
        });
    }
}
```

HTML

```
<input [(ngModel)]="hero.name" 
        [debounce]="3000" 
        (blur)="hero.name = $event.target.value"
        (ngModelChange)="onChange()"
        placeholder="name">
		
		
```