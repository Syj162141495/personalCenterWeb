<template>
  <div class="background2">
    <div class="module_title">健康事件</div>
    <!-- 代办任务  日程表 -->
    <div class="demo-app-main">
      <FullCalendar class="demo-app-calendar" :options="calendarOptions">
        <!-- <template #eventContent="arg">
          <b>{{ arg.timeText }}</b>
          <i>{{ arg.event.title }}</i>
        </template> -->
      </FullCalendar>
    </div>
    <InputForm @register="registerDrawer" />
  </div>
</template>
<script>
  import { defineComponent } from 'vue';
  import FullCalendar from '@fullcalendar/vue3';
  import dayGridPlugin from '@fullcalendar/daygrid';
  import timeGridPlugin from '@fullcalendar/timegrid';
  import interactionPlugin from '@fullcalendar/interaction';
  import locale from '@fullcalendar/core/locales/zh-cn';
  import listPlugin from '@fullcalendar/list';
  import { createEventId, eventsList } from './event-utils';
  // import InputForm from './form.vue';
  import InputForm from '/@/views/information/imagesUpload/form.vue';
  import { useDrawer } from '/@/components/Drawer';

  const [registerDrawer, { openDrawer }] = useDrawer();

  export default defineComponent({
    components: {
      FullCalendar,
      InputForm,
    },
    data() {
      return {
        calendarOptions: {
          plugins: [
            dayGridPlugin,
            timeGridPlugin,
            interactionPlugin, // needed for dateClick
            listPlugin,
          ],
          headerToolbar: {
            left: 'prev,next today',
            center: 'title',
            // right: 'dayGridMonth,timeGridWeek',
            right: 'dayGridMonth,timeGridWeek,timeGridDay,listWeek',
          },
          initialView: 'timeGridWeek',
          initialEvents: eventsList, // alternatively, use the `events` setting to fetch from a feed
          locale: locale,
          editable: true,
          selectable: true,
          selectMirror: true,
          dayMaxEvents: true,
          weekends: true,
          height: '100%',
          eventColor: '#378006',
          dayMaxEvents: true,
          // select: this.handleDateSelect,
          eventClick: this.handleEventClick,
          eventsSet: this.handleEvents,
          /* you can update a remote database when these fire:
        eventAdd:
        eventChange:
        eventRemove:
        */
        },
        currentEvents: [],
      };
    },
    methods: {
      handleWeekendsToggle() {
        this.calendarOptions.weekends = !this.calendarOptions.weekends; // update a property
      },
      handleDateSelect(selectInfo) {
        let title = prompt('Please enter a new title for your event');
        let calendarApi = selectInfo.view.calendar;

        calendarApi.unselect(); // clear date selection

        if (title) {
          calendarApi.addEvent({
            id: createEventId(),
            title,
            start: selectInfo.startStr,
            end: selectInfo.endStr,
            allDay: selectInfo.allDay,
          });
        }
      },
      handleEventClick(clickInfo) {
        // if (confirm(`Are you sure you want to delete the event '${clickInfo.event.title}'`)) {
        //   clickInfo.event.remove();
        // }
        console.log({ id: clickInfo.event.id });
        openDrawer(true, { id: clickInfo.event.id });
      },
      handleEvents(events) {
        this.currentEvents = events;
      },
      registerDrawer,
    },
  });
</script>
<style>
  .background2 {
    /* height: 75%; */
    /* background-color: #eaf9ff; */
    border-radius: 10px; /* 圆角半径 */
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2); /* 阴影样式 */
  }
  .demo-app-main {
    flex-grow: 1;
    padding: 3em;
    height: 100%;
    font-family:
      Arial,
      Helvetica Neue,
      Helvetica,
      sans-serif;
    font-size: 14px;
  }
</style>
