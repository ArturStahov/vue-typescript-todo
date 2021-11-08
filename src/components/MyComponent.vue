<template>
  <div>
    <p>{{ message.title }}</p>
  </div>
</template>

<script lang="ts">
import Vue, { PropType } from "vue";
import { ComplexMessage } from "./interface.Mycomponent";

 interface IProp {
          name:string;
          age:number;
        }

const MyComponent = Vue.extend({
  data() {
    return {
      name: "dfdfdf",
    };
  },
  methods: {


   getValue<T extends IProp, U extends keyof T>(obj:T,prop:U){
        return obj[prop]
       },

    myFync(): (number | string)[] {
      //если ми не знаем масив каких типов будет передан делаем Дженерик
      //Думай о дженериках как о аргументе функции в котором вы указиваєте тип других аргументов
      const revers = <T>(array: T[]) => {
        return [...array].reverse();
      };

      // теперь можна передавать любой тип в масиве (при вызове можно указивать а можно и не указывать)
      revers<number>([1, 2, 3, 4, 5]); //можна не писать <number>
      revers<string>(["dfd", "fff"]); //можна не писать <string>
      revers([{ s: 1 }, { b: 2 }]);

      // AB можно обозвать как угодно Генерик для параметров поштучних
      //теперь можна передавать любие типы в пропи
      const createArrayFrom = <A, B>(a: A, b: B) => {
        return [a, b];
      };

      const b = createArrayFrom("1", 2);

      //Дженерики в классаах
      interface ISate {
        user:Object;
        image:string;
      }

      class State <T extends ISate>{
        private state :T;
        constructor(initialState:T){
          this.state=initialState;
        }
        getState(){
          return this.state;
        }

        setState(newState: T){
          this.state=newState;
        }
      }

      const stateObj= new State({user:{},image:'dfd'});

      //  если функция должна вернуть визов на входящих параметрах
      // const getLength = <T extends { length: number }> (a: T) => {
      //   return a.length;
      // };
      // также только с интерфейсом
      interface ILength {
        length: number;
      }
      const getLength = <T extends ILength>(a: T) => {
        return a.length;
      };


        // keyof -- ключь в обьекте  
        interface IProp {
          name:string;
          age:number;
        }
       function getValue<T extends IProp, U extends keyof T>(obj:T,prop:U){
        return obj[prop]
       }

       const someProp = getValue({name:'Art',age:35},'name');

       
        //1) получаем ключь входящего значения или null
       function getKey<T extends object, U extends keyof T>(obj:T, value:T[U]):U|null {
         const key = (Object.keys(obj) as Array<U>).find(key=> obj[key] === value)
         return key || null
       }
       //2) получаем ключь входящего значения или null(тоже что и віше)
       function getKey2<T extends object>(obj:T, value:T[keyof T]):keyof T|null {
         const key = (Object.keys(obj) as Array<keyof T>).find(key=> obj[key] === value)
         return key || null
       }
       //  патчим входящий обьект
       function PatchFild<T extends object,U extends keyof T,V extends T[U]>(obj:T,field:U,value:V):T{
           return obj
       }
        PatchFild({f:'1'},'f',"3")

       const key = getKey({name:'Artur'},'Artur')

       
        // указиваем жестко тип в дженерик
       function format<T = string>(s?:T): T|undefined {
         return s
       }

       


       interface IFirstObj {
         a:string;
         getType:()=>string
       }

       interface ISomeObj {
         [key: string]:string
       }

      function addSumm <T extends IFirstObj,C extends ISomeObj>(a:T,b:C):object{
         return {...a,...b}
      }

      const newObj = addSumm({a:'dfdfd',getType(){return a}},{a:'sdsd'})

      interface IPerson {
        firstName: string;
        lastName: string;
      }
      const getFullName = <T extends IPerson>(person: T) => {
        return {
          ...person,
          fullName: `${person.firstName} ${person.lastName}`,
        };
      };

      //Дженерик интерфейс
      interface User<T> {
        id: T;
      }
      const mango: User<number> = { id: 2 }; // тут обезательно указивать тип
      const poly: User<string> = { id: "2" }; // тут обезательно указивать тип

      // тайпи для примитивов
      // значение может бить только одним из данних
      type ReqStatus = "request" | "success" | "error";
      type Cords = [number, number];
      type ReadOnly = readonly number[];

      interface ObjInterface {
        name: String;
        age: number;
        family?: [string]; // ? знак необезательного свойства в обьекте
        readonly hobbies?: [string];
      }

      const obj: ObjInterface = {
        name: "Vasya",
        age: 12,
      };


      //Работа с ДОМ елементами
      const pRef=document.querySelector('p') as HTMLParagraphElement;
      
      const handlerEvent = <T extends MouseEvent> (evt:T)=>{
        const target = evt.currentTarget as EventTarget;
        console.log(target)
      }

      pRef.addEventListener('click',handlerEvent)
      

      // енуми
      enum Size {
        medium, // default 0
        large, // default 1
        little, // default 2
      }

      enum SizeWithVallue {
        medium = "m",
        large = "b",
        little = "s",
      }
      const a: string = "sdfdf";

      if (a == SizeWithVallue.medium) {
      }

      const sum = (a: number, b: number): number => {
        return a + b;
      };

      // type SumFn = (a: number, b: number) => number;

      interface ISumFn {
        (a: number, b: number): void | number;
      }

      const sum2: ISumFn = (a, b) => {
        return a + b;
      };

      //если обект произвольной длини
      interface LargeObjInterface {
        [key: string]: number;
      }
      const largeObj: LargeObjInterface = {
        first: 1,
        two: 2,
        three: 3,
        four: 1, // and etc.
      };

      // только чтение массива
      const privateArray: ReadOnly = [1, 2, 3, 4];

      // покритие классов
      interface IParams {
        name?: string;
        selector: string[];
      }

      interface IClass {
        sizes: string;
        getSize(): string;
      }

      class Myclass implements IClass {
        public sizes: string;
        private someArray: string[];

        constructor({ name = "dfdf", selector }: IParams) {
          this.sizes = name;
          this.someArray = selector;
        }

        getSize() {
          return this.sizes;
        }
      }

      const my = new Myclass({ name: "fwefwf", selector: ["fsfsf"] });
      const size = my.getSize();

      const status: ReqStatus = "success";
      this.$emit("sdfdf", status);
      console.log(status);
      const cords: Cords = [234, 232323];
      return cords;
    },
  },
  props: {
    name: String,
    success: { type: String },
    callback: {
      type: Function as PropType<() => void>,
    },
    message: {
      type: Object as PropType<ComplexMessage>,
      required: true,
    },
  },
});

export default MyComponent;
</script>

<style scoped></style>
