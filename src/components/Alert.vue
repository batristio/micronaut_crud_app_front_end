<template>
    <div>
        <b-alert show>Default Alert</b-alert>

        <b-alert variant="success" show>Success Alert</b-alert>

        <b-alert v-model="showDismissibleAlert" variant="danger" dismissible>
            Dismissible Alert!
        </b-alert>

        <b-alert
                :show="dismissCountDown"
                dismissible
                variant="warning"
                @dismissed="dismissCountDown=0"
                @dismiss-count-down="countDownChanged"
        >
            <p>This alert will dismiss after {{ dismissCountDown }} seconds...</p>
        </b-alert>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                dismissSecs: 10,
                dismissCountDown: 0,
                showDismissibleAlert: false
            }
        },
        methods: {
            countDownChanged(dismissCountDown) {
                this.dismissCountDown = dismissCountDown
            },
            showAlert() {
                this.dismissCountDown = this.dismissSecs
            }
        }
    }
</script>