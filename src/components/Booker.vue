<template>
    <section class="booker">
        <div class="row justify-content-center">
            <div class="col-12">
                <h3>Booker</h3>
            </div>
            <div class="col-4">
                <div class="row text-center">
                    <div class="form-group col-12">
                        <label for="bookType" class="col-12 col-form-label text-left">Flight type</label>
                        <select v-model="bookType" @change="typeChange($event)" class="form-control" required>
                            <option value="oneWay">one-way flight</option>
                            <option value="return">return flight</option>
                        </select>
                    </div>
                    <div class="form-group col-12">
                        <input
                            id="startDate"
                            type="text"
                            :class="inputStartClass"
                            name="startDate"
                            value
                            autofocus
                            :disabled="startDateStatus"
                            v-on:input="validate()"
                            v-model="startDate"
                            :placeholder="dateFormat"
                        />
                    </div>
                    <div class="form-group col-12">
                        <input
                            id="returnDate"
                            type="text"
                            :class="inputClass"
                            name="returnDate"
                            value
                            :disabled="returnDateStatus"
                            v-on:input="validate()"
                            v-model="returnDate"
                            :placeholder="dateFormat"
                        />
                    </div>
                    <button type="submit" @click="book()" :disabled="addBook" class="btn btn-purple mr-auto ml-auto">Book</button>
                </div>
            </div>
        </div>
        
    </section>
</template>

<script>
export default {
    name: "Booker",
    data() {
        return {
            bookType: "oneWay",
            startDate: "",
            startDateStatus: false,
            returnDate: "",
            returnDateStatus: true,
            addBook: true,
            inputClass: "form-control",
            dateFormat: "YYYY-MM-DD",
            inputStartClass: "form-control"
        }
    },
    methods: {
        formatDate(currentDate) {
            let _currentDate = new Date(currentDate)
            const months = ['Enero','Febrero', 'Marzo', 'Abril', 'Mayo', 'Junio', 'Julio', 'Agosto', 'Septiembre', 'Octubre', 'Noviembre', 'Diciembre']
            let year = _currentDate.getFullYear()
            let date = _currentDate.getDate() + 1
            let monthName = months[_currentDate.getMonth()]
            return `${date} ${monthName} ${year}`
        },
        async book() {
            let messageStart = ""
            let messageReturn = ""
            if (this.startDate) {
                messageStart = await this.formatDate(this.startDate)
            }
            if (this.returnDate) {
                messageReturn = await this.formatDate(this.returnDate)
            }
            if (this.bookType == "oneWay") {
                alert(`Has programado un vuelo de ida para el ${messageStart}`)
            } else if (this.bookType == "return") {
                alert(`Has programado un vuelo de ida para el ${messageStart} y retorno el ${messageReturn}`)
            }
        },
        typeChange(ev) {
            if (ev.target.value == "oneWay") {
                this.startDateStatus = false
                this.returnDateStatus = true
            } else if (ev.target.value == "return") {
                this.startDateStatus = false
                this.returnDateStatus = false
                this.addBook = true
            }
        },
        validate() {
            let regDate = /^\d{4}[./-](0?[1-9]|1[012])[./-](0?[1-9]|[12][0-9]|3[01])$/
            if (this.bookType == "oneWay") {
                if (regDate.test(this.startDate)) {
                    this.addBook = false
                    this.inputStartClass = "form-control"
                } else {
                    this.inputStartClass = "form-control error-input"
                    this.addBook = true
                }
            } else if (this.bookType == "return") {
                let _start = ""
                let _return = ""
                if (this.startDate) {
                    _start = new Date(this.startDate)
                    _return = new Date(this.returnDate)

                    if (regDate.test(this.startDate)) {
                        this.addBook = false
                        this.inputStartClass = "form-control"
                    } else {
                        this.inputStartClass = "form-control error-input"
                        this.addBook = true
                    }

                    if (regDate.test(this.returnDate)) {
                        this.addBook = false
                        this.inputClass = "form-control"
                    } else {
                        this.inputClass = "form-control error-input"
                        this.addBook = true
                    }
    
                    if (_start > _return) {
                        this.inputClass = "form-control error-input"
                        this.addBook = true
                    } else {
                        this.inputClass = "form-control"
                        this.addBook = false
                    }
                }
            }
        }
    }
}
</script>

<style scoped>
.btn-purple {
    color: #fff;
    background-color: #6542f4;
    border-color: #6542f4;
}
.counter-number {
    font-size: 5rem;
}
.error-input {
    background-color: #e3559a;
    color: #fefefe;
}
</style>