# Langkah-langkah Implementasi Tugas Laravel: Layout, Routing, dan MVC

## Set Up Your Laravel Project
```
composer create-project laravel/laravel tugas1
cd tugas1
```

## Create the Main Layout
- Create a file resources/views/layout/base.blade.php
- Add the basic HTML structure: header, sidebar, @yield('content') content, and footer.

## Routing
In routes/web.php, define different types of routes

## Controller
Generate controller 
` php artisan make:controller Pertemuan1Controller`

## Genap Ganjil | Prima | Fibonacci
### Routing 
```
Route::prefix('/pertemuan1')->group(function(){
 Route::match(['get', 'post'], '/genap-ganjil', [Pertemuan1Controller::class, 'genapGanjil'])->name('genap-ganjil');
 Route::get('/fibbonaci',[Pertemuan1Controller::class,'fibonacci'])->name('fibonacci');
 Route::get('/prima', [Pertemuan1Controller::class, 'bilanganPrima'])->name('bilangan-prima');
 Route::get('/param', fn() => view('pertemuan1.param'))->name('param');
 Route::get('/param/{param1}', [Pertemuan1Controller::class, 'param1'])->name('param1');
 Route::get('/param/{param1}/{param2}', [Pertemuan1Controller::class, 'param2'])->name('param2');
});
```

### Controller
```
<?php

namespace App\Http\Controllers;
use Illuminate\Http\Request;
use App\Models\Number;

class Pertemuan1Controller extends Controller
{
    public function genapGanjil(Request $request){
        $numberDetails = [];
        if ($request->has('n')) {
            $validatedData = $request->validate([
                'n' => 'required|integer|min:1',
            ]);

            $n = $validatedData['n'];
            $numberDetails = Number::getGenapGanjil($n); //
        }
        return view('pertemuan1.genap-ganjil',compact('numberDetails'));
    }

    public function bilanganPrima(Request $request){
        $numberDetails = [];
        if ($request->has('n')) {
            $validatedData = $request->validate([
                'n' => 'required|integer|min:1',
            ]);

            $n = $validatedData['n'];
            $numberDetails = Number::getPrima($n);
        }
        return view('pertemuan1.bilangan-prima',compact('numberDetails'));
    }

    public function fibonacci(Request $request){
        $numberDetails = [];
        if ($request->has('n')) {
            $validatedData = $request->validate([
                'n' => 'required|integer|min:1',
            ]);

            $n = $validatedData['n'];
            $numberDetails = Number::getFibonaci($n);
        }
        return view('pertemuan1.fibonacci',compact('numberDetails'));
    }
    
    public function param1($param1 = ''){
        $data['param1'] = $param1;
        return view('pertemuan1.param1',compact('data'));
    }

    public function param2($param1 ='', $param2 =''){
        $data['param1'] = $param1;
        $data['param2'] = $param2;
        return view('pertemuan1.param2',compact('data'));
    }
}
```

## Visual Website
### Genap Ganjil
<img width="1440" alt="Screenshot 2025-04-18 at 11 33 16" src="https://github.com/user-attachments/assets/8fb8dc13-baf2-478d-9c4b-a560a8dad42c" />
### Fibonacci
<img width="1440" alt="Screenshot 2025-04-18 at 11 33 23" src="https://github.com/user-attachments/assets/c3acf20b-7b6a-4de7-a7f7-f6789b2387b5" />
### Bilangan Prima
<img width="1440" alt="Screenshot 2025-04-18 at 11 33 30" src="https://github.com/user-attachments/assets/b6dea4f7-50c7-49d6-bdd5-95b78d5a040f" />
### Parameter 
<img width="1440" alt="Screenshot 2025-04-18 at 11 33 57" src="https://github.com/user-attachments/assets/b84e03ff-a49c-4f86-88a8-73428b30c706" />

