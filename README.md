# DemoApp2
1. create a new project
    ng new project-name
    

2. create app module
    create: app-routing.module.ts
    	import { NgModule } from '@angular/core';
	import { RouterModule, Routes } from '@angular/router';

	const routes: Routes = [];
	@NgModule({
  	imports: [RouterModule.forChild(routes)],
  	exports: [RouterModule]
	})
	export class LayoutRoutingModule { }
	
	

3. create: app.module.ts
    	import { NgModule } from '@angular/core';
	import { CommonModule } from '@angular/common';
	import { LayoutRoutingModule } from './layout-routing.module';
	import { LayoutComponent } from './layout/layout.component';
	import { HeaderComponent } from './header/header.component';
	@NgModule({
  		declarations: [LayoutComponent, HeaderComponent],
  		imports: [CommonModule, LayoutRoutingModule],
	})
	export class LayoutModule {}


4. update: main.ts
    platformBrowserDynamic().bootstrapModule(AppModule).catch((err) => {});
    RESTART APP**


5. create layout module
    app > ng g m layout --routing
    app > cd layout > ng g c layout 

    app> ng g c header
    update: layoutmodule: 
    declarations: [
        LayoutComponent,
        HeaderComponent
      ],
      imports: [
        CommonModule,
        LayoutRoutingModule
      ]

      update:layoutcomponent:
            <app-header></app-header>
                    <p>layout works!</p>
            <router-outlet></router-outlet>
            
            
 6. update: app-routing.module.ts
       import { NgModule } from '@angular/core';
      import { RouterModule, Routes } from '@angular/router';
      import { LayoutComponent } from './layout/layout/layout.component';
      
      const routes: Routes = [
        {
          path: '',
          component: LayoutComponent,
          children: [
            {
              path: '',
              loadChildren: () =>
                import('./layout/layout.module').then((m) => m.LayoutModule),
            },
          ],
        },
      ];
      @NgModule({
        imports: [RouterModule.forRoot(routes, { useHash: true })],
        exports: [RouterModule],
      })
      export class AppRoutingModule {}
      
      
  7. Remove standalone property
  	remove standalone : true
  	remove imports:[]
