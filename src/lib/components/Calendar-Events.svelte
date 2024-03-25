<script>
// @ts-nocheck

    import { Modal, Content, Trigger}  from "sv-popup";
    import Event from "./Event-Calendar.svelte";
    import {
        selectedEvent,
        selectedDate,
    } from "../../stores/calendar.store";
    
    export let eventDayIndex;
    export let eventsForMonth;
    
    $: getEvents = (dayIndex) => {
      if (!dayIndex || !$eventsForMonth || !$selectedDate) {
        return;
      }
      const eventsForSelectedDate = $eventsForMonth.filter(
        (e = e.date.split("-")) =>
        
        Number(e[0]) === $selectedDate.getFullYear() &&
        Number(e[1]) === $selectedDate.getMonth() &&
        Number(e[2]) === eventDayIndex
    );
    return eventsForSelectedDate;
  };

  function toTime(date) {
    if (
      date.getHours() === 0 &&
      date.getMinutes() === 0 &&
      date.getSeconds() === 0
    ) {
      return "";
    }

    return date.toLocaleTimeString();
  }

  function eventClicked(event) {
        selectedEvent.set(
                event
        );

  }
</script>

{#each getEvents(eventDayIndex) as event}
  <Modal>
    <Content>
        <Event/>
    </Content>
    <Trigger>
        <button
            class="event"
            on:click={() => eventClicked(event.id)}
        >
          {event.title}
          <br />
          {toTime(event.Time)} - {toTime(event.endTime)}
        </button>
        
    </Trigger>
    
</Modal>
{/each}

<style>
  .event {
    background: #daddfb;
    padding: 5px;
    margin-bottom: 5px;
    border-bottom: 4px solid #636cee;
  }
</style>
