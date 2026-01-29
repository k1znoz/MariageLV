<script lang="ts">
	// Navigation sections
	const sections = [
		{ id: 'accueil', label: 'Accueil' },
		{ id: 'dates-lieux', label: 'Dates & Lieux' },
		{ id: 'deroule', label: 'Déroulé' },
		{ id: 'acces', label: 'Accès' },
		{ id: 'hebergements', label: 'Hébergements' },
		{ id: 'dresscode', label: 'Dress Code' },
		{ id: 'enfants', label: 'Enfants' },
		{ id: 'questionnaire', label: 'Questionnaire' },
		{ id: 'contact', label: 'Contact' }
	];

	// Hébergements data
	const hebergementsProches = [
		{ nom: 'Gîte Les Acacias', capacite: '4/5 pers.', distance: 'Village', contact: '06 63 06 86 25', lien: 'https://www.bourgogne-tourisme.com/locations-de-vacances/les-accacias' },
		{ nom: 'Chambre d\'hôtes rue d\'Enzia', capacite: '2/3 pers.', distance: 'Village', contact: '06 66 92 57 54', lien: 'https://fr.airbnb.be/rooms/1105049826838486653?source_impression_id=p3_1769673552_P33HaqyVreNwclia' },
		{ nom: 'Moulin du Cray', capacite: '2 pers.', distance: '1 km', contact: '03 85 25 13 87', lien: 'http://moulinducray.free.fr/' },
		{ nom: 'Maison d\'Hôte Terre des Barres', capacite: '-', distance: '2 km', contact: '06 99 37 48 06', lien: '' },
		{ nom: 'Gite-des-chatelaines', capacite: '-', distance: '2 km', contact: '', lien: 'https://www.bourgogne-tourisme.com/locations-de-vacances/gite-des-chatelaines' },
		{ nom: 'Gîte Les Volets Rouges', capacite: '5 pers.', distance: '2,5 km', contact: '06 48 59 17 40', lien: 'https://www.bourgogne-tourisme.com/locations-de-vacances/les-volets-rouges-4' },
		{ nom: 'Chambres d\'hôtes Sylvie Bouteille', capacite: '4/6 pers.', distance: '3 km', contact: '06 11 60 68 00', lien: 'https://www.tourismecharolaisbrionnais.fr/chambres-d-hotes/chambres-d-hotes-bouteille-sylvie--HLOBOU071V502HGD.html' },
		{ nom: 'Écuries La Villeneuve', capacite: 'Familial', distance: '3 km', contact: '06 22 48 91 43', lien: '' }
	];

	const hebergementsEloignes = [
		{ nom: 'Le Baugy\'te (dortoir)', capacite: '14 pers.', distance: '5 km', contact: '06 41 99 54 82', petit_budget: true, lien: 'https://www.baugyte.com/' },
		{ nom: 'Chambres d\'hôtes Les Pergolas', capacite: '3 ch.', distance: '5 km', contact: 'homelespergolas@gmail.com', lien: 'https://les-pergolas-chambres-dhotes.jimdosite.com/' },
		{ nom: 'Villa Léonie (Marcigny)', capacite: '24 pers.', distance: '5 km', contact: '06 13 31 36 57', lien: 'https://www.bourgogne-tourisme.com/locations-de-vacances/villa-leonie' },
		{ nom: 'Gîte de la Terre des Pierres', capacite: '14 pers.', distance: '5,5 km', contact: '06 69 34 59 86', lien: 'https://laterredespierres.fr/' },
		{ nom: 'Gîte Le Chalet (Sainte-Foy)', capacite: '28 pers.', distance: '8,5 km', contact: '06 07 25 84 23', lien: 'https://www.lechalet-saintefoy.fr/' },
		{ nom: 'La Grange de Marraine & le Fenil de Joanny', capacite: '15-22 pers.', distance: '11 km', contact: '06 52 15 86 20', lien: 'http://www.grangedemarraine.com/' },
		{ nom: 'Château de Martigny', capacite: 'Chambres & gîte', distance: '12 min', contact: '03 85 81 53 21', lien: 'https://chateaudemartigny.fr/' },
		{ nom: 'Château de la Chaix', capacite: '-', distance: '18 min', contact: '06  09 27 98 36 / chateaudelachaix@gmail.com', lien: 'https://www.chateau-de-la-chaix.com/' },
		{ nom: 'Château de Vaulx', capacite: '-', distance: '22 km', contact: '07 88 34 84 94 / barry@chateaudevaulx.com', lien: 'https://www.chateaudevaulx.com/cms/index.php/fr/' }
	];

	let mobileMenuOpen = $state(false);
	let lightboxImage = $state<string | null>(null);

	function openLightbox(src: string) {
		lightboxImage = src;
	}

	function closeLightbox() {
		lightboxImage = null;
	}
</script>

<svelte:head>
	<title>Laetitia & Valentin — Mariage</title>
	<meta name="description" content="Nous avons le plaisir de vous convier à notre mariage les 10 et 11 octobre 2026." />
</svelte:head>

<!-- Navigation -->
<nav class="fixed top-0 left-0 right-0 z-50 bg-[var(--color-cream)]/95 backdrop-blur-sm border-b border-[var(--color-sage)]/20">
	<div class="max-w-6xl mx-auto px-4">
		<div class="flex items-center justify-between h-16">
			<a href="#accueil" class="font-serif text-xl text-[var(--color-charcoal)]">L & V</a>
			
			<!-- Desktop menu -->
			<div class="hidden md:flex items-center gap-6">
				{#each sections as section}
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
				{#each sections as section}
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
		<div class="text-center max-w-2xl mx-auto">
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
					<p class="text-[var(--color-sage-dark)] font-medium mb-4">Samedi 10 & Dimanche 11 octobre</p>
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

			<!-- Proches -->
			<div class="mb-12">
				<h3 class="font-serif text-xl text-[var(--color-charcoal)] mb-6 flex items-center gap-2">
					<span class="w-2 h-2 bg-[var(--color-sage)] rounded-full"></span>
					À proximité immédiate
				</h3>
				<div class="grid sm:grid-cols-2 lg:grid-cols-4 gap-4">
					{#each hebergementsProches as h}
						<div class="bg-white rounded-xl p-5 shadow-sm border border-[var(--color-sage)]/10 hover:shadow-md transition-shadow flex flex-col">
							<h4 class="font-medium text-[var(--color-charcoal)] text-sm mb-2 leading-tight">{h.nom}</h4>
							<div class="space-y-1 text-xs text-[var(--color-charcoal)]/60 flex-1">
								{#if h.capacite !== '-'}
									<p>👥 {h.capacite}</p>
								{/if}
								<p>📍 {h.distance}</p>
								<p class="text-[var(--color-sage-dark)]">📞 {h.contact}</p>
							</div>
							{#if h.lien}
								<a 
									href={h.lien} 
									target="_blank" 
									rel="noopener noreferrer"
									class="mt-3 inline-flex items-center justify-center gap-1.5 text-xs font-medium text-white bg-[var(--color-sage-dark)] hover:bg-[var(--color-charcoal)] px-3 py-2 rounded-lg transition-colors"
								>
									<svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
										<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14" />
									</svg>
									Voir le site
								</a>
							{/if}
						</div>
					{/each}
				</div>
			</div>

			<!-- Plus éloignés -->
			<div>
				<h3 class="font-serif text-xl text-[var(--color-charcoal)] mb-6 flex items-center gap-2">
					<span class="w-2 h-2 bg-[var(--color-terracotta)] rounded-full"></span>
					À quelques kilomètres
				</h3>
				<div class="grid sm:grid-cols-2 lg:grid-cols-3 gap-4">
					{#each hebergementsEloignes as h}
						<div class="bg-white rounded-xl p-5 shadow-sm border border-[var(--color-sage)]/10 hover:shadow-md transition-shadow flex flex-col">
							{#if h.petit_budget}
								<span class="inline-block text-xs bg-[var(--color-sage)]/20 text-[var(--color-sage-dark)] px-2 py-0.5 rounded mb-2 w-fit">Petit budget</span>
							{/if}
							<h4 class="font-medium text-[var(--color-charcoal)] text-sm mb-2 leading-tight">{h.nom}</h4>
							<div class="space-y-1 text-xs text-[var(--color-charcoal)]/60 flex-1">
								{#if h.capacite !== '-'}
									<p>👥 {h.capacite}</p>
								{/if}
								<p>📍 {h.distance}</p>
								<p class="text-[var(--color-sage-dark)]">📞 {h.contact}</p>
							</div>
							{#if h.lien}
								<a 
									href={h.lien} 
									target="_blank" 
									rel="noopener noreferrer"
									class="mt-3 inline-flex items-center justify-center gap-1.5 text-xs font-medium text-white bg-[var(--color-sage-dark)] hover:bg-[var(--color-charcoal)] px-3 py-2 rounded-lg transition-colors"
								>
									<svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
										<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14" />
									</svg>
									Voir le site
								</a>
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
					Un <strong class="text-[var(--color-charcoal)]">mood board</strong> vous sera communiqué 
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
					Merci de votre compréhension 💛
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
	<p class="mt-1">Fait avec 💛</p>
</footer>
