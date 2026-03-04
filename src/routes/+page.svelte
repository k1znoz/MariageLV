<script lang="ts">
	import { onMount } from 'svelte';
	import { fade, fly } from 'svelte/transition';

	// Navigation sections
	const sections = [
		{ id: 'accueil', label: 'Accueil' },
		{ id: 'notre-histoire', label: 'Notre Histoire' },
		{ id: 'dates-lieux', label: 'Dates & Lieux' },
		{ id: 'deroule', label: 'Déroulé' },
		{ id: 'acces', label: 'Accès' },
		{ id: 'hebergements', label: 'Hébergements' },
		{ id: 'dresscode', label: 'Dress Code' },
		{ id: 'enfants', label: 'Enfants' },
		{ id: 'questionnaire', label: 'Questionnaire' },
		{ id: 'contact', label: 'Contact' }
	];

	// Hébergements data - À pied
	const hebergementsPied = [
		{ nom: 'Gîte Les Acacias', capacite: '4/5 pers.', distance: '2 min à pied', contact: '06 63 06 86 25', note: '435,60 € pour 2 nuits', lien: '' },
		{ nom: 'Chambre d\'hôtes rue d\'Enzia', capacite: '6/7 pers.', distance: 'Village', contact: '06 66 92 57 54', note: 'Airbnb', lien: '' },
		{ nom: 'Gîte des Pradelles', capacite: '19 pers. (7 ch.)', distance: '3 min à pied', contact: '', note: '90 €/chambre/nuit + petit-déj inclus', lien: 'https://www.gites-de-france.com/fr/bourgogne-franche-comte/saone-et-loire/les-pradelles-71g2185' }
	];

	// Hébergements data - Moins de 10 min
	const hebergementsMoins10 = [
		{ nom: 'Moulin du Cray', capacite: '2 pers.', distance: '1 km', contact: '03 85 25 13 87', lien: 'http://moulinducray.free.fr/' },
		{ nom: 'Maison d\'Hôtes Terre des Barres', capacite: '-', distance: '2 km', contact: '06 99 37 48 06', email: 'abeauchiere@gmail.com', lien: '' },
		{ nom: 'Chambres d\'hôtes La Cathelinée', capacite: '-', distance: '2 km', email: 'delphinemuth@gmail.com', lien: '' },
		{ nom: 'Gîte Les Volets Rouges', capacite: '5 pers. (3 ch.)', distance: '2,5 km', contact: '06 48 59 17 40', email: 'contactlachassagne@gmail.com', lien: '' },
		{ nom: 'Chambres d\'hôtes Sylvie Bouteille', capacite: '4/6 pers.', distance: '3 km', contact: '06 11 60 68 00', lien: '' },
		{ nom: 'Écuries La Villeneuve (Vindecy)', capacite: 'Familial', distance: '3 km', contact: '06 22 48 91 43', lien: '' },
		{ nom: 'Domaine du Martray', capacite: '12 pers.', distance: '5 min', lien: 'https://www.bourgogne-tourisme.com/locations-de-vacances/domaine-du-martray' },
		{ nom: 'Domaine de la Chassagne', capacite: '12 pers.', distance: '4 min', lien: 'https://domainedelachassagne.com/sejourner/' },
		{ nom: 'Villa Léonie (Marcigny)', capacite: '24 pers.', distance: '5 km', contact: '06 13 31 36 57', lien: 'https://www.gitedegroupe.fr/gite-groupe-BO-aa72.html' },
		{ nom: 'Là-haut sur la colline (Marcigny)', capacite: '-', distance: '6 km (8 min)', contact: '06 56 72 57 51', lien: 'https://www.lahautsurlacolline-marcigny.fr/' },
		{ nom: 'Gîte de la Terre des Pierres', capacite: '14 pers.', distance: '5,5 km (7 min)', contact: '06 69 34 59 86', email: 'laterredespierres@gmail.com', lien: '' },
		{ nom: 'Le Baugy\'te', capacite: '15 à 21 pers.', distance: '6 min', note: 'Dortoir possible', lien: 'https://www.airbnb.fr/rooms/642671832409492662' }
	];

	// Hébergements data - 10-20 min
	const hebergements10a20 = [
		{ nom: 'Gîte de Sermaize', capacite: '14 pers.', distance: '12 min', lien: 'https://www.gites-de-france.com/fr/bourgogne-franche-comte/saone-et-loire/gite-de-sermaize-71g1628' },
		{ nom: 'Gîte Le Chalet (Sainte-Foy)', capacite: '29 pers.', distance: '8,5 km (13 min)', contact: '06 07 25 84 23', lien: 'https://www.lechalet-saintefoy.fr/' },
		{ nom: 'Domaine de la Guinchère (L\'Hôpital-le-Mercier)', capacite: 'Gîte 12p + ch. 5p', distance: '10 km (11 min)', contact: '07 84 24 12 19', lien: 'https://www.domainedelaguinchere.com/fr' },
		{ nom: 'Les Jardins du Soussilange (Céron)', capacite: '2 suites (5p + 6p)', distance: '13 km (16 min)', lien: 'https://www.lesjardinsdessoussilanges.com/' },
		{ nom: 'La Grange de Marraine & Le Fenil de Joanny', capacite: '15-22 pers.', distance: '11 km', contact: '06 52 15 86 20', lien: 'http://www.grangedemarraine.com/' },
		{ nom: 'Château de Martigny', capacite: 'Chambres & gîte', distance: '12 min', contact: '03 85 81 53 21', lien: '' },
		{ nom: 'Château de la Chaix (Saint-Christophe-en-Brionnais)', capacite: '-', distance: '18 min', lien: 'https://www.chateau-de-la-chaix.com/' },
		{ nom: 'Château de Vaulx (Saint-Julien-de-Civry)', capacite: 'Gîtes, suites & ch.', distance: '22 km', lien: 'https://www.chateaudevaulx.com/' }
	];

	// Photos du couple
	const photos = [
		'/ressources/Pic/WhatsApp%20Image%202026-01-30%20at%2009.30.31.jpeg',
		'/ressources/Pic/WhatsApp%20Image%202026-01-30%20at%2009.30.32.jpeg',
		'/ressources/Pic/WhatsApp%20Image%202026-01-30%20at%2009.30.32%20(1).jpeg',
		'/ressources/Pic/WhatsApp%20Image%202026-01-30%20at%2009.30.32%20(2).jpeg',
		'/ressources/Pic/WhatsApp%20Image%202026-01-30%20at%2009.30.32%20(3).jpeg',
		'/ressources/Pic/WhatsApp%20Image%202026-01-30%20at%2009.30.33.jpeg',
		'/ressources/Pic/WhatsApp%20Image%202026-01-30%20at%2009.30.33%20(1).jpeg',
		'/ressources/Pic/WhatsApp%20Image%202026-01-30%20at%2009.30.33%20(2).jpeg',
		'/ressources/Pic/WhatsApp%20Image%202026-01-30%20at%2009.30.35.jpeg',
		'/ressources/Pic/WhatsApp%20Image%202026-01-30%20at%2009.30.37.jpeg'
	];

	let mobileMenuOpen = $state(false);
	let lightboxImage = $state<string | null>(null);
	let introOpen = $state(true);
	let introClosing = $state(false);
	let introStarted = $state(false);
	let introUseVideo = $state<boolean | null>(null);
	let introVideoFailed = $state(false);
	let introVideoEl = $state<HTMLVideoElement | null>(null);
	let introFallbackTimer: ReturnType<typeof setTimeout> | null = null;
	let introEndTimer: ReturnType<typeof setTimeout> | null = null;
	const introVideoSrc = '/ressources/vid/ouverture-lettre-scellee.mov';
	const introPoster = photos[0];

	function openLightbox(src: string) {
		lightboxImage = src;
	}

	function closeLightbox() {
		lightboxImage = null;
	}

	function finishIntro() {
		if (introClosing) return;
		introClosing = true;

		if (introEndTimer) {
			clearTimeout(introEndTimer);
		}

		introEndTimer = setTimeout(() => {
			introOpen = false;
		}, 620);
	}

	function handleIntroKeydown(e: KeyboardEvent) {
		if (e.key === 'Enter' || e.key === ' ') {
			e.preventDefault();
			startIntro();
		}
	}

	async function startIntro() {
		if (introClosing) return;

		if (introUseVideo === false || introVideoFailed) {
			finishIntro();
			return;
		}

		if (introUseVideo === null) return;

		if (introStarted || !introVideoEl) return;
		introStarted = true;

		if (introFallbackTimer) {
			clearTimeout(introFallbackTimer);
		}

		introFallbackTimer = setTimeout(() => {
			introVideoFailed = true;
			finishIntro();
		}, 9000);

		try {
			await introVideoEl.play();
		} catch {
			introVideoFailed = true;
			introStarted = false;
		}
	}

	onMount(() => {
		const probe = document.createElement('video');
		const canPlayQuickTime = probe.canPlayType('video/quicktime') !== '';
		const canPlayMp4 = probe.canPlayType('video/mp4') !== '';
		introUseVideo = canPlayQuickTime || canPlayMp4;

		return () => {
			if (introFallbackTimer) clearTimeout(introFallbackTimer);
			if (introEndTimer) clearTimeout(introEndTimer);
			document.body.style.overflow = '';
		};
	});

	$effect(() => {
		if (introOpen && introUseVideo && !introVideoFailed && introVideoEl && !introStarted) {
			startIntro();
		}
	});

	$effect(() => {
		document.body.style.overflow = introOpen ? 'hidden' : '';
	});


</script>

<svelte:head>
	<title>Laetitia & Valentin — Mariage</title>
	<meta name="description" content="Nous avons le plaisir de vous convier à notre mariage les 10 et 11 octobre 2026." />
</svelte:head>

{#if introOpen}
	<div
		class="intro-overlay fixed inset-0 z-[120] cursor-pointer overflow-hidden"
		class:opacity-0={introClosing}
		class:opacity-100={!introClosing}
		onclick={() => {
			if (introUseVideo && !introVideoFailed) {
				finishIntro();
				return;
			}
			if (introUseVideo === false || introVideoFailed) {
				finishIntro();
				return;
			}
		}}
		onkeydown={handleIntroKeydown}
		role="button"
		tabindex="0"
		aria-label="Ouvrir l'invitation"
	>
		{#if introUseVideo && !introVideoFailed}
			<video
				bind:this={introVideoEl}
				src={introVideoSrc}
				class="absolute inset-0 h-full w-full object-cover"
				muted
				playsinline
				autoplay
				preload="metadata"
				onended={() => {
					if (introFallbackTimer) clearTimeout(introFallbackTimer);
					finishIntro();
				}}
				onerror={() => {
					if (introFallbackTimer) clearTimeout(introFallbackTimer);
					introVideoFailed = true;
					introStarted = false;
				}}
			></video>
		{:else if introUseVideo === false || introVideoFailed}
			<img
				src={introPoster}
				alt="Laetitia et Valentin"
				class="absolute inset-0 h-full w-full object-cover"
			/>
		{:else}
			<div class="absolute inset-0 bg-black"></div>
		{/if}

		<div class="absolute inset-0 bg-black/45"></div>

		<div class="absolute inset-0 flex items-center justify-center px-6 text-center">
			<div class="max-w-md" in:fade={{ duration: 500 }}>
				<div class="mb-6 h-10" aria-hidden="true"></div>
				<p class="text-white/75 uppercase tracking-[0.35em] text-xs mb-5">Une invitation vous attend</p>
				<h2 class="font-serif text-white text-4xl md:text-5xl mb-4">Laetitia & Valentin</h2>
				<p class="text-white/80 text-sm">{introUseVideo && !introVideoFailed ? 'Touchez l’écran pour passer' : 'Touchez l’écran pour ouvrir'}</p>
			</div>
		</div>
	</div>
{/if}

<!-- Navigation -->
{#if !introOpen}
<nav class="fixed top-0 left-0 right-0 z-50 bg-[var(--color-cream)]/95 backdrop-blur-sm border-b border-[var(--color-sage)]/20">
	<div class="max-w-6xl mx-auto px-4">
		<div class="flex items-center justify-between h-16">
			<a href="#accueil" class="font-serif text-xl text-[var(--color-charcoal)]">L & V</a>
			
			<!-- Desktop menu -->
			<div class="hidden md:flex items-center gap-6">
				{#each sections as section (section.id)}
					<a 
						href="#{section.id}" 
						class="text-sm text-[var(--color-charcoal)]/70 hover:text-[var(--color-sage-dark)] transition-colors"
					>
						{section.label}
					</a>
				{/each}
			</div>

			<!-- Mobile menu button -->
			<button 
				class="md:hidden p-2" 
				onclick={() => mobileMenuOpen = !mobileMenuOpen}
				aria-label="Menu"
			>
				<svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
					{#if mobileMenuOpen}
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M6 18L18 6M6 6l12 12" />
					{:else}
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M4 6h16M4 12h16M4 18h16" />
					{/if}
				</svg>
			</button>
		</div>

		<!-- Mobile menu -->
		{#if mobileMenuOpen}
			<div class="md:hidden py-4 border-t border-[var(--color-sage)]/20">
				{#each sections as section (section.id)}
					<a 
						href="#{section.id}" 
						class="block py-2 text-sm text-[var(--color-charcoal)]/70 hover:text-[var(--color-sage-dark)]"
						onclick={() => mobileMenuOpen = false}
					>
						{section.label}
					</a>
				{/each}
			</div>
		{/if}
	</div>
</nav>

<main>
	<!-- HERO / ACCUEIL -->
	<section id="accueil" class="min-h-screen flex items-center justify-center px-4 pt-16 bg-gradient-to-b from-[var(--color-cream)] to-[var(--color-sage)]/10">
		<div class="text-center max-w-2xl mx-auto" in:fly={{ y: 20, duration: 700 }}>
			<p class="section-subtitle">Nous nous marions</p>
			<h1 class="font-serif text-5xl md:text-7xl font-medium text-[var(--color-charcoal)] mb-4">
				Laetitia <span class="text-[var(--color-gold)]">&</span> Valentin
			</h1>
			<div class="divider"></div>
			<p class="text-lg md:text-xl text-[var(--color-charcoal)]/80 mb-2">
				10 & 11 octobre 2026
			</p>
			<p class="text-base text-[var(--color-charcoal)]/60 mb-8">
				Gueugnon & Anzy-le-Duc, Bourgogne
			</p>
			<p class="text-base md:text-lg text-[var(--color-charcoal)]/70 leading-relaxed max-w-lg mx-auto mb-10">
				C'est avec une immense joie que nous vous invitons à partager ce moment unique avec nous. 
				Votre présence sera notre plus beau cadeau.
			</p>
			<a 
				href="#dates-lieux" 
				class="inline-flex items-center gap-2 text-[var(--color-sage-dark)] hover:text-[var(--color-charcoal)] transition-colors"
			>
				<span class="text-sm uppercase tracking-widest">Découvrir</span>
				<svg class="w-4 h-4 animate-bounce" fill="none" stroke="currentColor" viewBox="0 0 24 24">
					<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 14l-7 7m0 0l-7-7m7 7V3" />
				</svg>
			</a>
		</div>
	</section>

	<!-- PHOTO À L'HONNEUR -->
	<section class="py-20 px-4 bg-[var(--color-sage)]/5">
		<div class="max-w-4xl mx-auto">


			<div class="divider"></div>

			<!-- Photo mise en avant -->
			<div class="mt-12 flex justify-center">
				<button 
					type="button"
					onclick={() => openLightbox(photos[6])}
					class="group relative cursor-pointer"
				>
					<!-- Cadre décoratif extérieur -->
					<div class="absolute -inset-6 bg-gradient-to-br from-[var(--color-sage)]/20 to-[var(--color-rose)]/20 rounded-3xl blur-lg opacity-60 group-hover:opacity-100 transition-opacity duration-500"></div>
					<div class="absolute -inset-3 border-2 border-[var(--color-sage)]/30 rounded-2xl group-hover:border-[var(--color-sage)]/50 transition-colors duration-300"></div>
					
					<!-- Container photo principale -->
					<div class="relative bg-white p-3 md:p-4 rounded-xl shadow-2xl group-hover:shadow-[0_25px_60px_-15px_rgba(0,0,0,0.25)] transition-all duration-500">
						<img 
							src={photos[6]} 
							alt="Laetitia & Valentin" 
							class="max-w-full max-h-[60vh] w-auto h-auto rounded-lg object-contain"
						/>
						
						<!-- Overlay élégant au survol -->
						<div class="absolute inset-3 md:inset-4 bg-gradient-to-t from-black/40 via-transparent to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300 rounded-lg flex items-end justify-center pb-6">
							<span class="text-white font-script text-xl md:text-2xl drop-shadow-lg">Cliquez pour agrandir</span>
						</div>
					</div>
					

				</button>
			</div>

			<!-- Citation -->
			<p class="text-center mt-16 text-[var(--color-text-light)] italic font-light text-lg">
				"Le début de notre belle aventure ensemble"
			</p>
		</div>
	</section>

	
	<!-- NOTRE HISTOIRE -->
	<section id="notre-histoire" class="py-20 px-4 bg-white">
		<div class="max-w-5xl mx-auto">
			<p class="section-subtitle">Comment tout a commencé</p>
			<h2 class="section-title">Notre Histoire</h2>
			<div class="divider"></div>

			<div class="mt-12 columns-1 md:columns-2 lg:columns-3 gap-8 text-[var(--color-charcoal)]/80 text-justify leading-relaxed [column-rule:1px_solid_var(--color-sage)/20]">
				<p class="mb-4">Il était une fois, un aventurier rentrant des terres de Vercingetorix. Entre deux courbatures, il prit son téléphone et fit une dernière tentative à la recherche de l'âme sœur… et posa un « like » sur le profil d'une demoiselle.</p>

				<p class="mb-4">De son côté, lors d'un festin entre amie, elle découvrit un personnage aux milles visages : portant un ensemble banane douteux sur une première illustration, puis vêtu tel un motard aventurier, ou encore héros de rooftop torse nu, noble en costume, et troubadour en tee-shirt slogan. « Quel est donc cet étrange chevalier au sourire ensorcelant ? » songea-t-elle. Elle lika.</p>

				<p class="mb-4">Mais dans le royaume de Bumble, la dame doit écrire la première. Sachant qu'il revenait du Vietnam, contrée qu'elle allait explorer, elle lança : « Aurais-tu des conseils pour un voyage au Vietnam ? »</p>

				<p class="mb-4">À 16h06 précises, réponse immédiate. Itinéraires, montagnes, plages, deux-roues… Les messages pleuvaient. Était-ce un chevalier ou un agent de voyage ? Peu importe : au pire, le rendez-vous serait rentable.</p>

				<p class="mb-4">Trois jours plus tard, au Café Bohème, il attendait, ponctuel. Elle arriva — légèrement en retard, comme toute héroïne qui se respecte. Il se retourna. Et la flèche invisible frappa.</p>

				<p class="mb-4">Monsieur banane disparut. Apparut un héros à la veste d'aviateur et au sourire ravageur. Le temps suspendit son vol. Ils rirent, parlèrent, oublièrent même de manger, jusqu'à ce que le café les chasse.</p>

				<p class="mb-4">De retour chez elle, elle murmura à ses amies : « les filles c'est un désastre… » elle était… amoureuse.</p>

				<p class="mb-4">Puis arriva le message tant espéré : « Es-tu bien rentrée ? »</p>

				<p class="mb-4">Ils se revirent. Et depuis ce jour, ils ne se quittèrent plus.</p>

				<p class="mb-4">Comme quoi, même dans les contes modernes, tout peut commencer par… <strong class="text-[var(--color-sage-dark)]">un ensemble banane.</strong></p>
			</div>
		</div>
	</section>


	<!-- DATES & LIEUX -->
	<section id="dates-lieux" class="py-20 px-4">
		<div class="max-w-4xl mx-auto">
			<p class="section-subtitle">Où & Quand</p>
			<h2 class="section-title">Dates & Lieux</h2>
			<div class="divider"></div>

			<div class="grid md:grid-cols-2 gap-8 mt-12">
				<!-- Cérémonie -->
				<div class="bg-white rounded-2xl p-8 shadow-sm border border-[var(--color-sage)]/10">
					<div class="w-12 h-12 bg-[var(--color-sage)]/20 rounded-full flex items-center justify-center mb-4">
						<span class="text-2xl">⛪</span>
					</div>
					<h3 class="font-serif text-2xl text-[var(--color-charcoal)] mb-2">Cérémonie religieuse</h3>
					<p class="text-[var(--color-sage-dark)] font-medium mb-4">Samedi 10 octobre 2026</p>
					<div class="space-y-1 text-[var(--color-charcoal)]/70">
						<p class="font-medium text-[var(--color-charcoal)]">Église Saint-Maurice</p>
						<p>Place de l'église</p>
						<p>71130 Gueugnon</p>
					</div>
					<p class="mt-4 text-sm text-[var(--color-charcoal)]/60 flex items-center gap-2">
						<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
						</svg>
						Parking à proximité
					</p>
					<!-- Plan de parking -->
					<div class="mt-6">
						<p class="text-sm font-medium text-[var(--color-charcoal)] mb-2 flex items-center gap-2">
							<span>🅿️</span> Plan des parkings
						</p>
						<button type="button" onclick={() => openLightbox('/ressources/parkingEglise.jpeg')} class="w-full">
							<img 
								src="/ressources/parkingEglise.jpeg" 
								alt="Plan des parkings autour de l'église de Gueugnon" 
								class="rounded-xl w-full border border-[var(--color-sage)]/20 cursor-pointer hover:shadow-lg transition-shadow"
							/>
						</button>
						<p class="text-xs text-[var(--color-charcoal)]/50 mt-2 text-center">Cliquez pour agrandir</p>
					</div>
				</div>

				<!-- Réception -->
				<div class="bg-white rounded-2xl p-8 shadow-sm border border-[var(--color-sage)]/10">
					<div class="w-12 h-12 bg-[var(--color-terracotta)]/20 rounded-full flex items-center justify-center mb-4">
						<span class="text-2xl">🥂</span>
					</div>
					<h3 class="font-serif text-2xl text-[var(--color-charcoal)] mb-2">Vin d'honneur & Réception</h3>
					<p class="text-[var(--color-sage-dark)] font-medium mb-4">Samedi 10 octobre 2026</p>
					<div class="space-y-1 text-[var(--color-charcoal)]/70">
						<p class="font-medium text-[var(--color-charcoal)]">Les Salles du Prieuré</p>
						<p>Le Bourg – Le Prieuré</p>
						<p>71110 Anzy-le-Duc</p>
					</div>
					<p class="mt-4 text-sm text-[var(--color-charcoal)]/60 flex items-center gap-2">
						<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
						</svg>
						Parking sur place
					</p>
					<!-- Plan de parking -->
					<div class="mt-6">
						<p class="text-sm font-medium text-[var(--color-charcoal)] mb-2 flex items-center gap-2">
							<span>🅿️</span> Plan des parkings
						</p>
						<button type="button" onclick={() => openLightbox('/ressources/parkingPrieure.jpeg')} class="w-full">
							<img 
								src="/ressources/parkingPrieure.jpeg" 
								alt="Plan des parkings autour des Salles du Prieuré à Anzy-le-Duc" 
								class="rounded-xl w-full border border-[var(--color-sage)]/20 cursor-pointer hover:shadow-lg transition-shadow"
							/>
						</button>
						<p class="text-xs text-[var(--color-charcoal)]/50 mt-2 text-center">Cliquez pour agrandir</p>
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- DÉROULÉ DU WEEK-END -->
	<section id="deroule" class="py-20 px-4 bg-[var(--color-sage)]/10">
		<div class="max-w-3xl mx-auto">
			<p class="section-subtitle">Le programme</p>
			<h2 class="section-title">Déroulé du week-end</h2>
			<div class="divider"></div>

			<div class="mt-12 space-y-8">
				<!-- Samedi -->
				<div class="bg-white rounded-2xl p-8 shadow-sm">
					<h3 class="font-serif text-2xl text-[var(--color-charcoal)] mb-6 flex items-center gap-3">
						<span class="w-10 h-10 bg-[var(--color-sage)]/20 rounded-full flex items-center justify-center text-sm font-sans">Sam</span>
						Samedi 10 octobre
					</h3>
					<div class="space-y-4">
						<div class="flex gap-4">
							<div class="w-16 text-[var(--color-sage-dark)] font-medium text-sm">14h30</div>
							<div>
								<p class="font-medium text-[var(--color-charcoal)]">Cérémonie religieuse</p>
								<p class="text-sm text-[var(--color-charcoal)]/60">Église Saint-Maurice, Gueugnon</p>
							</div>
						</div>
						<div class="rounded-xl bg-[var(--color-sage)]/10 border border-[var(--color-sage)]/20 p-5">
							<p class="font-medium text-[var(--color-charcoal)] mb-2">🏍️ Appel aux motards</p>
							<p class="text-sm text-[var(--color-charcoal)]/75 leading-relaxed">Amis motards,</p>
							<p class="text-sm text-[var(--color-charcoal)]/75 leading-relaxed">Nous vous invitons à enfourcher vos motos pour escorter les mariés et former une haie d’honneur pleine de bruit, de chrome et d’émotion.</p>
							<p class="text-sm text-[var(--color-charcoal)]/75 leading-relaxed">Venez écrire avec nous ce moment unique… moteur allumé et cœur grand ouvert.</p>
						</div>
						<div class="flex gap-4">
							<div class="w-16 text-[var(--color-sage-dark)] font-medium text-sm">16h00</div>
							<div>
								<p class="font-medium text-[var(--color-charcoal)]">Trajet vers la réception</p>
								<p class="text-sm text-[var(--color-charcoal)]/60">Environ 40 minutes</p>
							</div>
						</div>
						<div class="flex gap-4">
							<div class="w-16 text-[var(--color-sage-dark)] font-medium text-sm">17h00</div>
							<div>
								<p class="font-medium text-[var(--color-charcoal)]">Vin d'honneur</p>
								<p class="text-sm text-[var(--color-charcoal)]/60">Les Salles du Prieuré, Anzy-le-Duc</p>
							</div>
						</div>
						<div class="flex gap-4">
							<div class="w-16 text-[var(--color-sage-dark)] font-medium text-sm">20h00</div>
							<div>
								<p class="font-medium text-[var(--color-charcoal)]">Dîner & Soirée dansante</p>
								<p class="text-sm text-[var(--color-charcoal)]/60">Jusqu'au bout de la nuit ✨</p>
							</div>
						</div>
					</div>
				</div>

				<!-- Dimanche -->
				<div class="bg-white rounded-2xl p-8 shadow-sm">
					<h3 class="font-serif text-2xl text-[var(--color-charcoal)] mb-6 flex items-center gap-3">
						<span class="w-10 h-10 bg-[var(--color-terracotta)]/20 rounded-full flex items-center justify-center text-sm font-sans">Dim</span>
						Dimanche 11 octobre
					</h3>
					<div class="space-y-4">
						<div class="flex gap-4">
							<div class="w-16 text-[var(--color-sage-dark)] font-medium text-sm">11h00</div>
							<div>
								<p class="font-medium text-[var(--color-charcoal)]">Brunch convivial</p>
								<p class="text-sm text-[var(--color-charcoal)]/60">Pour prolonger le bonheur ensemble</p>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- ACCÈS & TRAJETS -->
	<section id="acces" class="py-20 px-4">
		<div class="max-w-3xl mx-auto">
			<p class="section-subtitle">Comment venir</p>
			<h2 class="section-title">Accès & Trajets</h2>
			<div class="divider"></div>

			<div class="mt-12 space-y-6">
				<div class="bg-white rounded-2xl p-8 shadow-sm border border-[var(--color-sage)]/10">
					<h3 class="font-serif text-xl text-[var(--color-charcoal)] mb-4 flex items-center gap-3">
						<span class="text-2xl">🚗</span>
						Trajet entre les lieux
					</h3>
					<p class="text-[var(--color-charcoal)]/70 mb-4">
						Le trajet entre l'église de Gueugnon et la salle de réception d'Anzy-le-Duc prend 
						<strong class="text-[var(--color-charcoal)]">environ 40 minutes</strong>.
					</p>
					<p class="text-sm text-[var(--color-charcoal)]/60">
						Nous vous invitons à prévoir ce temps de route et à covoiturer si possible.
					</p>
				</div>

				<!-- Alerte Péage -->
				<div class="bg-[var(--color-terracotta)]/10 rounded-2xl p-8 border border-[var(--color-terracotta)]/30">
					<h3 class="font-serif text-xl text-[var(--color-charcoal)] mb-4 flex items-center gap-3">
						<span class="text-2xl">⚠️</span>
						Péage en flux libre
					</h3>
					<p class="text-[var(--color-charcoal)]/80 mb-4">
						L'autoroute est équipée d'un <strong>péage en flux libre ALIAE</strong> (sans barrière).
					</p>
					<div class="bg-white rounded-xl p-4">
						<p class="text-sm text-[var(--color-charcoal)]/70">
							<strong class="text-[var(--color-charcoal)]">Important :</strong> Le paiement doit être effectué 
							<strong>sous 48h</strong> en ligne sur le site ALIAE, ou automatiquement si vous disposez d'un télépéage.
						</p>
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- HÉBERGEMENTS -->
	<section id="hebergements" class="py-20 px-4 bg-[var(--color-sage)]/10">
		<div class="max-w-5xl mx-auto">
			<p class="section-subtitle">Où dormir</p>
			<h2 class="section-title">Hébergements</h2>
			<div class="divider"></div>
			<p class="text-center text-[var(--color-charcoal)]/70 max-w-xl mx-auto mb-12">
				Voici une sélection d'hébergements à proximité du lieu de réception. 
				N'hésitez pas à réserver rapidement !
			</p>

			<!-- À pied -->
			<div class="mb-12">
				<h3 class="font-serif text-xl text-[var(--color-charcoal)] mb-6 flex items-center gap-2">
					<span class="text-xl">🚶</span>
					À pied (idéalement situés)
				</h3>
				<div class="grid sm:grid-cols-2 lg:grid-cols-3 gap-4">
					{#each hebergementsPied as h (h.nom)}
						<div class="bg-white rounded-xl p-5 shadow-sm border border-[var(--color-sage)]/10 hover:shadow-md transition-shadow flex flex-col">
							<h4 class="font-medium text-[var(--color-charcoal)] text-sm mb-2 leading-tight">{h.nom}</h4>
							<div class="space-y-1 text-xs text-[var(--color-charcoal)]/60 flex-1">
								{#if h.capacite && h.capacite !== '-'}
									<p>👥 {h.capacite}</p>
								{/if}
								<p>📍 {h.distance}</p>
								{#if h.contact}
									<p class="text-[var(--color-sage-dark)]">📞 {h.contact}</p>
								{/if}
								{#if h.note}
									<p class="text-[var(--color-terracotta)] font-medium">💡 {h.note}</p>
								{/if}
							</div>
							{#if h.lien}
								<button
									type="button"
									onclick={() => window.open(h.lien, '_blank', 'noopener,noreferrer')}
									class="mt-3 inline-flex items-center justify-center gap-1.5 text-xs font-medium text-white bg-[var(--color-sage-dark)] hover:bg-[var(--color-charcoal)] px-3 py-2 rounded-lg transition-colors"
								>
									<svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
										<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14" />
									</svg>
									Voir le site
								</button>
							{/if}
						</div>
					{/each}
				</div>
			</div>

			<!-- Plus éloignés -->
			<div class="mb-12">
				<h3 class="font-serif text-xl text-[var(--color-charcoal)] mb-6 flex items-center gap-2">
					<span class="text-xl">🚗</span>
					À moins de 10 minutes en voiture
				</h3>
				<div class="grid sm:grid-cols-2 lg:grid-cols-4 gap-4">
					{#each hebergementsMoins10 as h (h.nom)}
						<div class="bg-white rounded-xl p-5 shadow-sm border border-[var(--color-sage)]/10 hover:shadow-md transition-shadow flex flex-col">
							{#if h.note}
								<span class="inline-block text-xs bg-[var(--color-sage)]/20 text-[var(--color-sage-dark)] px-2 py-0.5 rounded mb-2 w-fit">{h.note}</span>
							{/if}
							<h4 class="font-medium text-[var(--color-charcoal)] text-sm mb-2 leading-tight">{h.nom}</h4>
							<div class="space-y-1 text-xs text-[var(--color-charcoal)]/60 flex-1">
								{#if h.capacite && h.capacite !== '-'}
									<p>👥 {h.capacite}</p>
								{/if}
								<p>📍 {h.distance}</p>
								{#if h.contact}
									<p class="text-[var(--color-sage-dark)]">📞 {h.contact}</p>
								{/if}
								{#if h.email}
									<p class="text-[var(--color-sage-dark)]">✉️ {h.email}</p>
								{/if}
							</div>
							{#if h.lien}
								<button
									type="button"
									onclick={() => window.open(h.lien, '_blank', 'noopener,noreferrer')}
									class="mt-3 inline-flex items-center justify-center gap-1.5 text-xs font-medium text-white bg-[var(--color-sage-dark)] hover:bg-[var(--color-charcoal)] px-3 py-2 rounded-lg transition-colors"
								>
									<svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
										<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14" />
									</svg>
									Voir le site
								</button>
							{/if}
						</div>
					{/each}
				</div>
			</div>

			<!-- 10-20 min -->
			<div>
				<h3 class="font-serif text-xl text-[var(--color-charcoal)] mb-6 flex items-center gap-2">
					<span class="text-xl">🚗</span>
					À 10–20 minutes en voiture
				</h3>
				<div class="grid sm:grid-cols-2 lg:grid-cols-4 gap-4">
					{#each hebergements10a20 as h (h.nom)}
						<div class="bg-white rounded-xl p-5 shadow-sm border border-[var(--color-sage)]/10 hover:shadow-md transition-shadow flex flex-col">
							<h4 class="font-medium text-[var(--color-charcoal)] text-sm mb-2 leading-tight">{h.nom}</h4>
							<div class="space-y-1 text-xs text-[var(--color-charcoal)]/60 flex-1">
								{#if h.capacite && h.capacite !== '-'}
									<p>👥 {h.capacite}</p>
								{/if}
								<p>📍 {h.distance}</p>
								{#if h.contact}
									<p class="text-[var(--color-sage-dark)]">📞 {h.contact}</p>
								{/if}
							</div>
							{#if h.lien}
								<button
									type="button"
									onclick={() => window.open(h.lien, '_blank', 'noopener,noreferrer')}
									class="mt-3 inline-flex items-center justify-center gap-1.5 text-xs font-medium text-white bg-[var(--color-sage-dark)] hover:bg-[var(--color-charcoal)] px-3 py-2 rounded-lg transition-colors"
								>
									<svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
										<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14" />
									</svg>
									Voir le site
								</button>
							{/if}
						</div>
					{/each}
				</div>
			</div>
		</div>
	</section>

	<!-- DRESS CODE -->
	<section id="dresscode" class="py-20 px-4">
		<div class="max-w-2xl mx-auto text-center">
			<p class="section-subtitle">Tenue</p>
			<h2 class="section-title">Dress Code</h2>
			<div class="divider"></div>

			<div class="mt-10 bg-white rounded-2xl p-10 shadow-sm border border-[var(--color-sage)]/10">
				<div class="w-16 h-16 bg-[var(--color-gold)]/10 rounded-full flex items-center justify-center mx-auto mb-6">
					<span class="text-3xl">👗</span>
				</div>
				<p class="text-[var(--color-charcoal)]/80 text-lg leading-relaxed">
					Une <strong class="text-[var(--color-charcoal)]">palette de couleur</strong> vous sera communiquée 
					avec le faire-part afin de vous guider dans le choix de votre tenue.
				</p>
				<p class="mt-4 text-sm text-[var(--color-charcoal)]/60">
					Restez à l'écoute ! ✨
				</p>
			</div>
		</div>
	</section>

	<!-- ENFANTS & GARDE -->
	<section id="enfants" class="py-20 px-4 bg-[var(--color-sage)]/10">
		<div class="max-w-2xl mx-auto text-center">
			<p class="section-subtitle">Les petits</p>
			<h2 class="section-title">Enfants & Garde</h2>
			<div class="divider"></div>

			<div class="mt-10 bg-white rounded-2xl p-10 shadow-sm">
				<div class="w-16 h-16 bg-[var(--color-sage)]/20 rounded-full flex items-center justify-center mx-auto mb-6">
					<span class="text-3xl">👶</span>
				</div>
				<p class="text-[var(--color-charcoal)]/80 text-lg mb-8">
					Les enfants sont les bienvenus pour tout le week-end !
				</p>

				<div class="grid sm:grid-cols-2 gap-4 text-left">
					<div class="bg-[var(--color-cream)] rounded-xl p-5">
						<p class="font-medium text-[var(--color-charcoal)] mb-1">👩‍👧 Nounous disponibles</p>
						<p class="text-sm text-[var(--color-charcoal)]/60">
							Des nounous seront présentes pour s'occuper des enfants.
						</p>
					</div>
					<div class="bg-[var(--color-cream)] rounded-xl p-5">
						<p class="font-medium text-[var(--color-charcoal)] mb-1">🏠 Salle dédiée</p>
						<p class="text-sm text-[var(--color-charcoal)]/60">
							Un espace de garde est prévu à côté de la salle de dîner.
						</p>
					</div>
				</div>

				<div class="mt-8 p-4 bg-[var(--color-terracotta)]/10 rounded-xl border border-[var(--color-terracotta)]/20">
					<p class="text-sm text-[var(--color-charcoal)]/70">
						<strong class="text-[var(--color-charcoal)]">À noter :</strong> 
						Les frais de garde seront à la charge des parents.
					</p>
				</div>

				<p class="mt-6 text-sm text-[var(--color-charcoal)]/60 italic">
					Merci de votre compréhension ❤️
				</p>
			</div>
		</div>
	</section>

	<!-- QUESTIONNAIRE -->
	<section id="questionnaire" class="py-20 px-4">
		<div class="max-w-2xl mx-auto text-center">
			<p class="section-subtitle">Confirmez votre présence</p>
			<h2 class="section-title">Questionnaire</h2>
			<div class="divider"></div>

			<div class="mt-10 bg-gradient-to-br from-[var(--color-sage)]/20 to-[var(--color-terracotta)]/10 rounded-2xl p-10">
				<p class="text-[var(--color-charcoal)]/80 text-lg mb-8">
					Pour nous aider à organiser au mieux cette journée, merci de remplir le questionnaire ci-dessous.
				</p>
				<p class="text-sm text-[var(--color-charcoal)]/60 italic mb-6">
					Si vous venez en moto, pensez à le préciser dans le questionnaire 🏍️
				</p>
				<a 
					href="https://docs.google.com/forms/d/e/1FAIpQLSewyccDsNKdWDfoCYeaBDZAnuDI57GG-U_aRBujMzAdl7Kf0A/viewform"
					target="_blank"
					rel="noopener noreferrer"
					class="inline-flex items-center gap-2 bg-[var(--color-sage-dark)] hover:bg-[var(--color-charcoal)] text-white px-8 py-4 rounded-full font-medium transition-colors shadow-lg hover:shadow-xl"
				>
					Répondre au questionnaire
					<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" />
					</svg>
				</a>
				<p class="mt-6 text-sm text-[var(--color-charcoal)]/60">
					Le questionnaire prend moins de 2 minutes à compléter.
				</p>
			</div>
		</div>
	</section>

	<!-- CONTACT -->


</main>

<!-- Lightbox -->
{#if lightboxImage}
	<div 
		class="fixed inset-0 z-[100] bg-black/90 flex items-center justify-center p-4"
		onclick={closeLightbox}
		onkeydown={(e) => e.key === 'Escape' && closeLightbox()}
		role="dialog"
		aria-modal="true"
		tabindex="-1"
	>
		<button 
			type="button"
			class="absolute top-4 right-4 text-white/80 hover:text-white transition-colors p-2"
			onclick={closeLightbox}
			aria-label="Fermer"
		>
			<svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
			</svg>
		</button>
		<!-- svelte-ignore a11y_no_noninteractive_element_interactions -->
		<!-- svelte-ignore a11y_click_events_have_key_events -->
		<img 
			src={lightboxImage} 
			alt="Plan agrandi" 
			class="max-w-full max-h-[90vh] object-contain rounded-lg shadow-2xl"
			onclick={(e) => e.stopPropagation()}
		/>
	</div>
{/if}

<!-- Footer -->
<footer class="bg-[var(--color-charcoal)] text-white/40 py-6 px-4 text-center text-sm border-t border-white/10">
	<p>Laetitia & Valentin — 10 & 11 octobre 2026</p>
	<p class="mt-1">Fait avec ❤️</p>
</footer>
{/if}

<style>
	.intro-overlay {
		transition: opacity 620ms cubic-bezier(0.22, 1, 0.36, 1);
	}
</style>
