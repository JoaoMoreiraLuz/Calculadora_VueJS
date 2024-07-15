<script setup>
import { reactive } from 'vue';


const estado = reactive({
    numeroA: '',
    numeroB: '',
    operacoes: {
        somar: (a,b) => a + b,
        subtrair: (a, b) => a - b,
        multiplicar: (a, b) => a * b,
        dividir: (a, b) => (b !== 0 ? a / b : 'Divisao por zero'),
    },
    resultado: 0,
})

const calculo = () => {
    const {numeroA, numeroB, operacao} = estado;
    const num1 = parseFloat(numeroA);
    const num2 = parseFloat(numeroB);
    estado.resultado = !isNaN(num1) && !isNaN(num2) ? estado.operacoes[operacao](num1, num2) : 'Argumentos precisam ser números.';
};
</script>

<template>
    <div class="container">
        <div class="row">
            <div class="col-md-6">
                <input type="text" class="form-control mb-3" v-model="estado.numeroA" @input="calculo">
            </div>
            <div class="col-md-6">
                <input type="text" class="form-control mb-3" v-model="estado.numeroB" @input="calculo">
            </div>
        </div>

        <select v-model="estado.operacao" @change="calculo">
            <option value="somar">Somar</option>
            <option value="subtrair">subtrair</option>
            <option value="multiplicar">multiplicar</option>
            <option value="dividir">dividir</option>
        </select>
        <p class="text-primary fs-5 mt-3">
            Resultado: {{ estado.resultado }}
        </p>
    </div>
</template>