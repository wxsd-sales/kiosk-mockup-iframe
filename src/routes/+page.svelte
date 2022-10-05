<script>
	import { page } from '$app/stores';

	import Render from '../components/render.svelte';
	import initialView from '../images/initial-view.jpeg';
	import calenderView from '../images/calender-view.jpeg';
	import bookingView from '../images/booking-view.jpeg';
	import bookingSearchingView from '../images/booking-searching.jpeg';
	import bookingFoundView from '../images/booking-found.jpeg';
	import bookCaseView from '../images/book-case.jpeg';
	import bookCaseTimeView from '../images/time-picker.jpeg';
	import bookCaseStationPicker from '../images/station-picker.jpeg';
	import bookCaseStationSelected from '../images/select-station.jpeg';
	import bookCaseRoomPicker from '../images/time-picker-with-station.jpeg';
	import bookCaseRoomSelected from '../images/book-case-room-selected.jpeg';
	import scheduleView from '../images/schedule-view.jpeg';
	import scheduledSuccessfullyView from '../images/booking-submitted.jpeg';
	import '../app.css';

	let displayHomeView = true;
	let displayCalView = false;
	let displayBookingView = false;
	let displayBookingSearchingView = false;
	let displayBookingFoundView = false;
	let displayBookCaseView = false;
	let displayBookCaseTimeView = false;
	let displayBookCaseStationPicker = false;
	let displayBookCaseStationSelected = false;
	let displayBookCaseRoomPicker = false;
	let displayBookCaseRoomSelected = false;
	let displayScheduleView = false;
	let displayScheduledSuccessfullyView = false;

	const removeAllView = () => {
		displayBookingView = false;
		displayHomeView = false;
		displayCalView = false;
		displayBookingSearchingView = false;
		displayBookingFoundView = false;
		displayBookCaseView = false;
		displayBookCaseTimeView = false;
		displayBookCaseStationPicker = false;
		displayBookCaseStationSelected = false;
		displayBookCaseRoomPicker = false;
		displayBookCaseRoomSelected = false;
		displayScheduleView = false;
		displayScheduledSuccessfullyView = false;
	};

	const sipAddress = $page.url.searchParams.get('sipAddress') || 'fahabbou@cisco.com';
</script>

{#if displayHomeView}
	<Render url={initialView} />
	<canvas
		class="join-meeting"
		on:click={() => {
			window.location.href = `sip:${sipAddress}`;
		}}
	/>
{:else if displayCalView}
	<Render url={calenderView} />
	<canvas
		class="join-scheduled-meeting"
		on:click={() => {
			window.location.href = `sip:${sipAddress}`;
		}}
	/>
{:else if displayBookingView}
	<Render url={bookingView} />
	<canvas
		class="booking-view-canvas"
		on:click={() => {
			removeAllView();
			displayBookingSearchingView = true;
		}}
	/>
{:else if displayBookingSearchingView}
	<Render url={bookingSearchingView} />
	<canvas
		class="booking-view-canvas"
		on:click={() => {
			removeAllView();
			displayBookingFoundView = true;
		}}
	/>
{:else if displayBookingFoundView}
	<Render url={bookingFoundView} />
	<canvas
		class="booking-found-view-canvas"
		on:click={() => {
			removeAllView();
			displayBookCaseView = true;
		}}
	/>
{:else if displayBookCaseView}
	<Render url={bookCaseView} />
	<canvas
		class="time-picker-canvas"
		on:click={() => {
			removeAllView();
			displayBookCaseTimeView = true;
		}}
	/>
{:else if displayBookCaseTimeView}
	<Render url={bookCaseTimeView} />
	<canvas
		class="station-finder-input"
		on:click={() => {
			removeAllView();
			displayBookCaseStationPicker = true;
		}}
	/>
{:else if displayBookCaseStationPicker}
	<Render url={bookCaseStationPicker} />
	<canvas
		class="station-select"
		on:click={() => {
			removeAllView();
			displayBookCaseStationSelected = true;
		}}
	/>
{:else if displayBookCaseStationSelected}
	<Render url={bookCaseStationSelected} />
	<canvas
		class="station-select-box"
		on:click={() => {
			removeAllView();
			displayBookCaseRoomPicker = true;
		}}
	/>
{:else if displayBookCaseRoomPicker}
	<Render url={bookCaseRoomPicker} />
	<canvas
		class="room-picker"
		on:click={() => {
			removeAllView();
			displayBookCaseRoomSelected = true;
		}}
	/>
{:else if displayBookCaseRoomSelected}
	<Render url={bookCaseRoomSelected} />
	<canvas
		class="next-button"
		on:click={() => {
			removeAllView();
			displayScheduleView = true;
		}}
	/>
{:else if displayScheduleView}
	<Render url={scheduleView} />
	<canvas
		class="next-button"
		on:click={() => {
			removeAllView();
			displayScheduledSuccessfullyView = true;
		}}
	/>
{:else if displayScheduledSuccessfullyView}
	<Render url={scheduledSuccessfullyView} />
	<canvas
		class="call-button"
		on:click={() => {
			window.location.href = `sip:${sipAddress}`;
		}}
	/>
	<canvas
		class="cancel-button"
		on:click={() => {
			removeAllView();
			displayHomeView = true;
		}}
	/>
{/if}

<div class="side-menu">
	<canvas
		class="home"
		on:click={() => {
			removeAllView();
			displayHomeView = true;
		}}
	/>
	<canvas
		class="cal"
		on:click={() => {
			removeAllView();
			displayCalView = true;
		}}
	/>
	<canvas
		class="book"
		on:click={() => {
			removeAllView();
			displayBookingView = true;
		}}
	/>
</div>

<style>
	.join-meeting {
		position: fixed;
		width: 55rem;
		height: 3.5rem;
		border-radius: 0.25rem;
		top: 17.5rem;
		right: 60rem;
	}

	.join-scheduled-meeting {
		position: fixed;
		width: 20rem;
		height: 3.5rem;
		border-radius: 0.25rem;
		top: 31.5rem;
		right: 12rem;
	}

	.side-menu {
		z-index: 1;
		position: fixed;
		right: 1.75rem;
		top: 12rem;
		width: 2rem;
		height: 12rem;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
	}

	.home {
		width: 2rem;
		height: 2rem;
	}

	.cal {
		width: 2rem;
		height: 2rem;
	}

	.book {
		width: 2rem;
		height: 2rem;
	}

	.booking-view-canvas {
		position: fixed;
		width: 48rem;
		height: 4rem;
		border-radius: 0.5rem;
		top: 20.5rem;
		right: 32rem;
	}

	.booking-found-view-canvas {
		position: fixed;
		width: 48rem;
		height: 3rem;
		border-radius: 0.25rem;
		top: 28rem;
		right: 32rem;
	}

	.time-picker-canvas {
		position: fixed;
		width: 2rem;
		height: 2rem;
		border-radius: 0.25rem;
		top: 46.5rem;
		right: 48rem;
	}

	.station-finder-input {
		position: fixed;
		width: 23rem;
		height: 2rem;
		border-radius: 0.25rem;
		top: 61rem;
		right: 50rem;
	}

	.station-select {
		position: fixed;
		width: 32rem;
		height: 4rem;
		border-radius: 0.25rem;
		top: 20.5rem;
		right: 47rem;
	}

	.station-select-box {
		position: fixed;
		width: 22rem;
		height: 12rem;
		border-radius: 0.25rem;
		top: 25.5rem;
		right: 55rem;
	}

	.room-picker {
		position: fixed;
		width: 15rem;
		height: 20rem;
		border-radius: 0.25rem;
		top: 40rem;
		right: 81rem;
	}

	.next-button {
		position: fixed;
		width: 2rem;
		height: 2rem;
		border-radius: 0.25rem;
		top: 6.5rem;
		right: 29.25rem;
	}

	.call-button {
		position: fixed;
		width: 12rem;
		height: 3rem;
		border-radius: 0.25rem;
		top: 38rem;
		right: 50rem;
	}

	.cancel-button {
		position: fixed;
		width: 2rem;
		height: 2rem;
		border-radius: 0.25rem;
		top: 5.5rem;
		right: 82.5rem;
	}
</style>
