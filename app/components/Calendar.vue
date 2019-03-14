<template>
    <Page class="page">
        <ActionBar title="DoDo." class="action-bar">
            <NavigationButton text="DoDo" android.systemIcon="ic_menu_back"
                @tap="goBack" />
            <ActionItem text="todo" android.systemIcon="ic_menu_add" @tap="goTodo" />
        </ActionBar>
        <StackLayout id="calendar" orientation="vertical" width="100%" height="100%">

            <RadCalendar height="1000px" viewmode="month" :selectionMode="selectionMode" />
        </StackLayout>
    </Page>
</template>

<script>
    import Vue from "nativescript-vue";
    import HelloWorld from "./HelloWorld";
    import RadCalendarPlugin from "nativescript-ui-calendar/vue";
    Vue.use(RadCalendarPlugin);
    import {
        CalendarSelectionMode
    } from "nativescript-ui-calendar";
    import Todo from "./Todo";

    export default {
        methods: {
            goBack() {
                this.$navigateTo(HelloWorld, {
                    clearHistory: true
                });
            },
			 goTodo() { this.$navigateTo(Todo, { 
                 clearHistory: true 
                 });
            }
        }
    };
</script>

<style>
</style>