<template>
    <Page class="page">
        <ActionBar title="DoDo" class="action-bar">
            <NavigationButton text="DoDo" android.systemIcon="ic_menu_back"
                @tap="goBack" />
            <ActionItem text="calendar" android.systemIcon="ic_menu_my_calendar"
                @tap="goCalendar" />
        </ActionBar>
        <TabView height="100%" androidTabsPosition="bottom">
            <TabViewItem title="To Do" id="todo">
                <!-- Positions an input field, a button, and the list of tasks in a vertical stack. -->
                <StackLayout orientation="vertical" width="100%" height="100%">

                    <GridLayout columns="2*,*" rows="*" width="100%" height="25%">
                        <TextField col="0" row="0" v-model="textFieldValue"
                            hint="Lisa uus ülesanne..." editable="true"
                            @returnPress="onButtonTap" textWrap="true" />
                        <!-- Configures the text field and ensures that pressing Return on the keyboard produces the same result as tapping the button. -->
                        <Button col="1" row="0" text="Lisa" @tap="onButtonTap"
                            backgroundColor="lightgreen" />
                    </GridLayout>

                    <ListView separatorColor="transparent" class="list-group"
                        for="todo in todos" @itemTap="onItemTap" style="height:75%">
                        <v-template>
                            <Label id="active-task" :text="todo.name" class="list-group-item-heading"
                                textWrap="true" />
                        </v-template>
                    </ListView>
                </StackLayout>
            </TabViewItem>
            <TabViewItem title="Tehtud">
                <ListView class="list-group" for="done in dones" @itemTap="onDoneTap"
                    style="height:75%" separatorColor="transparent">
                    <v-template>
                        <Label id="completed-task" :text="done.name" class="list-group-item-heading"
                            textWrap="true" />
                    </v-template>
                </ListView>
            </TabViewItem>
        </TabView>
    </Page>
</template>

<script>
    import HelloWorld from "./HelloWorld";
    import Calendar from "./Calendar";
    import DatePicker from "tns-core-modules/ui/date-picker";

    export default {
        methods: {
            onItemTap: function(args) {
                action("Mida soovid ülesandega teha?", "Tühista", [
                    "Märgi lõpetatuks",
                    "Kustuta"
                ]).then(result => {
                    console.log(result); // Logs the selected option for debugging.
                    switch (result) {
                        case "Märgi lõpetatuks":
                            this.dones.unshift(args.item); // Places the tapped active task at the top of the completed tasks.
                            this.todos.splice(args.index, 1); // Removes the tapped active  task.
                            break;
                        case "Kustuta":
                            this.todos.splice(args.index, 1); // Removes the tapped active task.
                            break;
                        case "Tühista" || undefined: // Dismisses the dialog
                            break;
                    }
                });
            },

            onDoneTap: function(args) {
                action("Mida soovid ülesandega teha?", "Tühista", [
                    "Ennista Todo",
                    "Kustuta"
                ]).then(result => {
                    console.log(result); // Logs the selected option for debugging.
                    switch (result) {
                        case "Ennista Todo":
                            this.todos.unshift(args.item); // Places the tapped completed task at the top of the to do tasks.
                            this.dones.splice(args.index, 1); // Removes the tapped completed task.
                            break;
                        case "Kustuta":
                            this.dones.splice(args.index, 1); // Removes the tapped completed task.
                            break;
                        case "Tühista" || undefined: // Dismisses the dialog
                            break;
                    }
                });
            },

            onButtonTap() {
                if (this.textFieldValue === "") return; // Prevents users from entering an empty string.
                console.log("Lisatud uus ülesanne: " + this.textFieldValue +
                    "."); // Logs the newly added task in the console for debugging.
                this.todos.unshift({
                    name: this.textFieldValue
                }); // Adds tasks in the ToDo array. Newly added tasks are immediately shown on the screen.
                this.textFieldValue = ""; // Clears the text field so that users can start adding new tasks immediately.
            },

            goBack() {
                this.$navigateTo(HelloWorld, {
                    clearHistory: true
                });
            },
            goCalendar() {
                this.$navigateTo(Calendar, {
                    clearHistory: true
                });
            }
        },

        data() {
            return {
                dones: [],
                todos: [],
                textFieldValue: ""
            };
        }
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

    TextField {
        font-size: 20;
        color: #53ba82;
        margin-top: 10;
        margin-bottom: 10;
        margin-right: 5;
        margin-left: 20;
    }

    Button {
        font-size: 20;
        font-weight: bold;
        color: white;
        background-color: #53ba82;
        height: 50;
        margin-top: 10;
        margin-bottom: 10;
        margin-right: 10;
        margin-left: 10;
        border-radius: 20px;
    }

    #active-task {
        font-size: 20;
        font-weight: bold;
        color: #53ba82;
        margin-left: 20;
        padding-top: 5;
        padding-bottom: 10;
    }

	 #completed-task { 
         font-size: 20; 
         color: pink;
         margin-left: 20; 
         padding-top: 5; 
         padding-bottom: 10; 
         text-decoration: line-through;
	}
</style>