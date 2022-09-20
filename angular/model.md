# model

in models

#### deserializable.model.ts
```
export interface Deserializable {
    deserialize(input: any): this;
}
```

#### other model
```
import {Other} from "./other.model";
import {Deserializable} from "./deserializable.model";

export class This implements Deserializable {
    id: number;
    name: string;
    other: Other;

    deserialize(input: any) {
        Object.assign(this, input);
        return this;
    }
}

```
