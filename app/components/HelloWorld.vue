<template>
    <Page class="page">
        <ActionBar title="DoDo." class="action-bar">
            <ActionItem text="calendar" android.systemIcon="ic_menu_my_calendar"
                @tap="goCalendar" />
        </ActionBar>
        <StackLayout orientation="vertical" width="100%" height="100%">
            <GridLayout columns="*,* " rows="auto, auto" class="m-y-30 m-x-20">
                <!-- Date Today -->
                <Label :text="day" row="0" col="0" class="weekday" />
                <Label :text="date + '. ' + month + ', ' + year" row="1" col="0"
                    class="date" color="#C2C8E6" />
            </GridLayout>
            <!-- Task Buttons -->
            <GridLayout columns="*,*,*" rows="*,*,*" width="100%" height="60%">
                <Button class="actionbutton" col="0" row="1" text="Vaba aeg"
                    editable="true" @tap="free" id="free" backgroundColor="lightgreen"></Button>
                <Button class="actionbutton" col="1" row="0" text="Töö"
                    editable="true" @tap="work" id="work" backgroundColor="lightblue"></Button>
                <Button class="actionbutton" col="2" row="1" text="Kodu"
                    editable="true" @tap="home" id="home" backgroundColor="pink"></Button>
                <Button class="actionbutton" col="1" row="2" text="Kool"
                    editable="true" @tap="school" id="school" backgroundColor="yellow"></Button>
        </StackLayout>
    </Page>
</template>

<script>
    import Vue from "nativescript-vue";
    import Calendar from "./Calendar";
    import Todo from "./Todo";

    export default {
        created() {
            var currentDate = new Date();
            var day = currentDate.getDay();
            var date = currentDate.getDate();
            var year = currentDate.getFullYear();
            var weekdays = new Array(7);
            weekdays[0] = "Pühapäev";
            weekdays[1] = "Esmaspäev";
            weekdays[2] = "Teisipäev";
            weekdays[3] = "Kolmapäev";
            weekdays[4] = "Neljapäev";
            weekdays[5] = "Reede";
            weekdays[6] = "Laupäev";
            var dayName = weekdays[day];
            this.day = dayName;
            this.date = date;
            this.year = year;
            var month = new Array();
            month[0] = "Jaanuar";
            month[1] = "Veebruar";
            month[2] = "Märts";
            month[3] = "Aprill";
            month[4] = "Mai";
            month[5] = "Juuni";
            month[6] = "Juuli";
            month[7] = "August";
            month[8] = "September";
            month[9] = "Oktoober";
            month[10] = "November";
            month[11] = "Detsember";
            var monthName = month[currentDate.getMonth()];
            this.month = monthName;
        },
        methods: {
            work() {
                this.$navigateTo(Todo, {
                    clearHistory: true
                });
            },

            free() {
                this.$navigateTo(Todo, {
                    clearHistory: true
                });
            },

            school() {
                this.$navigateTo(Todo, {
                    clearHistory: true
                });
            },

            home() {
                this.$navigateTo(Todo, {
                    clearHistory: true
                });
            },
            goCalendar() {
                this.$navigateTo(Calendar, {
                    clearHistory: true
                });
            }
        }

        //data() {
        //  return {};
        //},
    };
</script>

<style scoped>
    .home-panel {
        vertical-align: center;
        font-size: 20;
        margin: 15;
    }

    .description-label {
        margin-bottom: 15;
    }

    Button {
        font-size: 20;
        color: #7e7e7e;
    }

</style>