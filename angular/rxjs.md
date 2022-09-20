# RxJS
> unorganized

# Rx JS
## create observables in RxJS6

xxx.service.ts

Import {.Observable, from } from ‘rxjs’

export class XxxService {
	getXxx():Observable<string>{
		return from(FOOD_LIST)
	}
}


app.component.ts

constructor(private xxxService: XxxService) {}

demo(){
	this.foodService.getFoods()
	.subscribe( x => {
		console.log(‘value: ’, $(x))
	})
}


## using pipeable operators in RxJS5
getXxxUppercase():Observable<string>{
	return Observable.from(FOOD_LIST).map( x => x.toUpperCase() )
}

## using pipeable operators in RxJS6
return from(FOOD_LIST).piple(
	passOnlyStartswinVowel()
	map(x => x.toUpperCase())
)

## create custom operators
Import {.Observable } from “rxjs”;

export const passOnlyStartswinVowel = () => <T>(source:Observable<T>) =>
	new Observable<T> observer => {
		return source.subscribe({
			next(x){
				let char = x.toString().charAt(0).toLowerCase()
				if (char == “a” ||
				    char == “e” ||
				    char == “i” ||
				    char == “o” ||
				    char == “u”) {

					observer.next(x)
				}
			},
			error(err) {
				observer.error(err)
			},
			complete() {
				observer.complete()
			}
		})
	}

## promise
In service
getXXX_p():Promise<any> {
	// RxJS 5
	let myObs::Observable<any> = this.http.get(“http://localhost:3000/foods”)
	return myObs.toPromise()

	// RxJS 6
	return this.http.get(“http://localhost:3000/foods”).toPromise()

}

In app
demo_getXXX_promise() {
	this.xxxService.getXXX_p()
	.then( xxx = > console.log(xxx))
	.catch( err => console.log(“error: ${err}”))
}

## Handling Errors on the Observer Side
In service
observer.error(new Error(“Error”))

In app
demo_getXXX_getXXXX_e() {
	this.xxxService.getFoods_e()
	.subscribe(
		next => { console.log(“received emitted value: ${next}”) },
		error => { console.log(“received an error: ${error}”) },
		() => {console.log(“received is complete”)}
}


## Handling Errors on the Observable Side

getFoods_e():Observable<any>{
	return Observable.create( observer => {
		let index = 0;

		setInterval( () => {
			let nextFood = FOOD_LIST(index)
			if(nextFood) {
				observer.next(nextFood)
				index++;
			}
			else {
				observer.error(new Error(“Array access error”))
			}
		}, 1000)
	})
	.catch( err => {
		console.log(“there is same error with the observable.”)
		return Observable.of(FOOD_LIST)
	})
}

