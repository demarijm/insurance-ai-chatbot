<script lang="ts">
	import { onMount } from 'svelte';
	// import { theme } from './theme';

	let firstName = 'John';
	let lastName = 'Doe';
	let workEmail = 'sdw@dfw.ce';
	let personalEmail = 'sdw@dfw.ce';
	let employerDistrict = 'Baltimore County Public Schools';
	let school = '';
	let mobileNumber = '3';

	async function init() {
		const theme = await fetch(
			'https://mediafiles.botpress.cloud/34ffb0c3-deb4-4b2f-9906-e80e1b5fc39c/webchat/v2/theme.json'
		).then((response) => response.json());

		// Ensure window.botpress is defined (may need <script src="...botpress.bundle.js"> in index.html)
		window.botpress.init({
			theme,
			clientId: '0bcc6702-fe27-4a3d-b149-0710b414996b',
			user: {
				data: {
					firstName: firstName,
					lastName: lastName,
					email: workEmail,
					personalEmail: personalEmail,
					employerDistrict: employerDistrict,
					school: school,
					mobileNumber: mobileNumber
				}
			},
			botId: '34ffb0c3-deb4-4b2f-9906-e80e1b5fc39c',
			style:
				'https://mediafiles.botpress.cloud/34ffb0c3-deb4-4b2f-9906-e80e1b5fc39c/webchat/v2/style.css',
			configuration: {
				botDescription: 'This is a Webchat demo bot.',
				botName: 'Webchat Demo',
				composerPlaceholder: 'Chat with me!',
				email: {
					title: 'contact@botpress.com',
					link: 'mailto:contact@botpress.com'
				},
				phone: {
					title: '555 555 555',
					link: 'tel:555 555 555'
				},
				privacyPolicy: {
					title: 'Privacy policy',
					link: 'https://botpress.com/legal/privacy-statement'
				},
				termsOfService: {
					title: 'Terms of service',
					link: 'https://botpress.com/legal/terms-of-service'
				},
				website: {
					title: 'https://botpress.com',
					link: 'https://botpress.com'
				}
			}
		});

		window.botpress.open();
	}

	onMount(() => {
		const params = new URLSearchParams(window.location.search);
		firstName = params.get('firstName') || '';
		lastName = params.get('lastName') || '';
		workEmail = params.get('workEmail') || '';
		personalEmail = params.get('personalEmail') || '';
		employerDistrict = params.get('employerDistrict') || '';
		school = params.get('school') || '';
		mobileNumber = params.get('mobileNumber') || '';
		init();
	});
</script>

<style global>
	html,
	body {
		margin: 0;
		padding: 0;
		height: 100%;
		width: 100%;
		overflow: hidden; /* optional, helps if you don't want any scrollbar */
	}

	.webchat {
		position: fixed;
		top: 0;
		left: 0;
		height: 100vh;
		width: 100vw;
	}
</style>
