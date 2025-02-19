<script lang="ts">
	import SideNav from '$components/politicians/SideNav.svelte';
	import General from '$components/icons/GeneralIcon.svelte';
	import Politician from '$components/icons/PoliticianIcon.svelte';
	import Vote from '$components/icons/VoteIcon.svelte';
	import PartyDetail from '$components/politicians/PartyDetail.svelte';
	import PositionStatus from '$components/politicians/PositionStatus.svelte';
	import Section from '$components/politicians/Section.svelte';
	import Share from '$components/Share/Share.svelte';
	import VotingResultTag from '$components/VotingResultTag/VotingResultTag.svelte';
	import { Breadcrumb, BreadcrumbItem, Button, InlineNotification } from 'carbon-components-svelte';
	import ArrowRight from 'carbon-icons-svelte/lib/ArrowRight.svelte';
	import ArrowUpRight from 'carbon-icons-svelte/lib/ArrowUpRight.svelte';
	import scrollama from 'scrollama';
	import { onMount } from 'svelte';

	import DownloadData from '$components/DownloadData/DownloadData.svelte';

	export let data;
	const { politician, agreedVoting, disagreedVoting, votingAbsentStats, totalProposedBill } = data;

	const groupBy = <T, K extends string>(arr: T[], groupFn: (element: T) => K): Record<K, T[]> =>
		arr.reduce(
			(r, v, _i, _a, k = groupFn(v)) => ((r[k] || (r[k] = [])).push(v), r),
			{} as Record<K, T[]>
		);
	const safePercent = (n: number, outOf: number) => Math.round((n / (outOf || 1)) * 10000) / 100;

	const age = new Date(Date.now() - politician.birthdate.getTime()).getFullYear() - 1970;
	const parties = groupBy(politician.partyRoles, (role) => role.party.name);
	const currentParty = politician.partyRoles.find((e) => !e.endedAt);
	const partyCount = Object.keys(parties).length;
	const currentRoles = politician.assemblyRoles.filter((e) => !e.endedAt);

	let currentNavElementIndex = 0;
	onMount(() => {
		if (window.matchMedia('(min-width: 672px)').matches) {
			const scroller = scrollama();

			scroller
				.setup({
					step: '.politician-section',
					// @ts-expect-error Documentation บอกว่าใช้ string ที่มี px ได้ https://github.com/russellsamora/scrollama#:~:text=number%20(0%20%2D%201%2C%20or%20string%20with%20%22px%22)
					offset: '33px'
				})
				.onStepEnter((response) => {
					currentNavElementIndex = response.index;
				});

			return scroller.destroy;
		}
	});
</script>

<Breadcrumb
	noTrailingSlash
	class="px-4 py-2 body-compact-01 [&>.bx--breadcrumb]:flex [&>.bx--breadcrumb]:flex-wrap"
>
	<BreadcrumbItem href="/">หน้าหลัก</BreadcrumbItem>
	<BreadcrumbItem href="/politicians/{politician.id}" isCurrentPage
		>{politician.firstname}</BreadcrumbItem
	>
</Breadcrumb>
<header class="px-4 py-8 md:px-16 md:py-12">
	<div class="relative w-[120px] h-[120px] mb-4">
		<img
			class="rounded-full overflow-hidden w-full h-full object-cover"
			src={politician.avatar}
			alt={politician.firstname + ' ' + politician.lastname}
			width="120"
			height="120"
			loading="lazy"
			decoding="async"
		/>
		{#if currentParty}
			<img
				class="absolute right-0 bottom-0 rounded-full overflow-hidden w-[32px] h-auto aspect-square bg-white border border-gray-30 border-solid object-contain"
				src={currentParty.party.logo}
				alt={currentParty.party.name}
				width="32"
				height="32"
				loading="lazy"
				decoding="async"
			/>
		{/if}
	</div>
	<div class="flex flex-col gap-8 md:flex-row md:gap-16">
		<div class="flex-1 flex flex-col gap-2">
			<h1 class="fluid-heading-05">
				{politician.prefix}
				{politician.firstname}
				{politician.lastname}
			</h1>
			<PositionStatus isActive={politician.isActive} />
			{#if currentRoles.length > 0}
				<h2 class="heading-01 -mb-2">ตำแหน่งปัจจุบัน</h2>
				<ul class="body-01 list-disc ml-8">
					{#each currentRoles as role, idx (idx)}
						<!-- TODO: add link -->
						<li>
							{role.role} ใน
							<a class="text-black" href="/">{role.assembly.name} ชุดที่ {role.assembly.term}</a>
						</li>
					{/each}
				</ul>
			{/if}
		</div>
		<div class="flex flex-col gap-2">
			<DownloadData links={[{ label: 'ผลการลงมติรายคน', url: '/' }]} />
			<p class="label-01 text-gray-60">อัปเดตข้อมูล: 18 ส.ค. 2566</p>
			<!-- TODO: add link -->
			<a href="/" class="mr-auto helper-text-01"> ที่มาและข้อจำกัดข้อมูล </a>
			<Share label="แชร์ประวัติ" />
		</div>
	</div>
</header>

<div
	class="flex flex-col items-start gap-4 p-4 min-h-screen bg-[--party] md:flex-row md:gap-8 md:py-8 md:px-16 heading-01"
	style:--party={currentParty?.party.color ?? '#F4F4F4'}
>
	<SideNav
		{currentNavElementIndex}
		assemblyRolesLength={politician.assemblyRoles.length}
		{partyCount}
		agreedVoting={agreedVoting.total}
		disagreedVoting={disagreedVoting.total}
		absentTotal={votingAbsentStats.absentVoting}
	/>
	<div class="flex-1 flex flex-col gap-6 w-full min-w-0">
		<Section id="personal" title="ข้อมูลพื้นฐาน">
			<General slot="icon" size="32" />
			<div>
				<p>
					<span class="heading-02">เพศ</span>
					{politician.sex} <span class="heading-02">ปีเกิด</span>
					{politician.birthdate.getFullYear() + 543} ({age} ปี)
				</p>
				{#if politician.educations.length > 0}
					<span class="heading-02">การศึกษา</span>
					<ul class="ml-8 list-disc">
						{#each politician.educations as education, idx (idx)}
							<li>{education}</li>
						{/each}
					</ul>
				{/if}
				{#if politician.previousOccupations.length > 0}
					<span class="heading-02">อาชีพเดิม</span>
					<ul class="ml-8 list-disc">
						{#each politician.previousOccupations as oldjob, idx (idx)}
							<li>{oldjob}</li>
						{/each}
					</ul>
				{/if}
			</div>
			<hr class="border-0 border-solid border-gray-20 border-t w-full m-0 box-border" />
			<div>
				<ul class="mb-1">
					<li>
						<span class="heading-02">ทรัพย์สิน</span>
						{politician.assetValue.toLocaleString('th-TH')} บาท
					</li>
					<li>
						<span class="heading-02">หนี้สิน</span>
						{politician.debtValue.toLocaleString('th-TH')} บาท
					</li>
				</ul>
				<!-- TODO: Add link -->
				<a
					href="/"
					class="mr-auto helper-text-01 flex gap-2 items-center w-fit"
					target="_blank"
					rel="nofollow noopener noreferrer"
				>
					<span>ตรวจสอบประวัติทางธุรกิจ</span>
					<ArrowUpRight />
				</a>
			</div>
			{#if politician.contacts.length > 0}
				<hr class="border-0 border-solid border-gray-20 border-t w-full m-0 box-border" />
				<div>
					<span class="heading-02">ช่องทางติดต่อ</span>
					<ul class="flex flex-wrap gap-3 helper-text-01">
						{#each politician.contacts as contact (contact.label)}
							<li>
								<a href={contact.url} target="_blank" rel="nofollow noopener noreferrer">
									{contact.label}
								</a>
							</li>
						{/each}
					</ul>
				</div>
			{/if}
		</Section>
		<Section id="politics" title="ประวัติทางการเมือง">
			<Politician slot="icon" size="32" />
			<p slot="header-extension" class="label-01 text-gray-60">
				หมายเหตุ: ข้อมูลย้อนหลังถึงปี 2562
			</p>
			{#if politician.assemblyRoles.length > 0}
				<div>
					<h3 class="heading-02">{politician.assemblyRoles.length} ตำแหน่งทางการเมือง</h3>
					<ul class="ml-8 list-disc">
						{#each politician.assemblyRoles as role, idx (idx)}
							<li>
								{role.role}
								<!-- TODO: add links -->
								<a class="text-black" href="/">
									{role.assembly.abbreviation} ชุดที่ {role.assembly.term}
								</a>
								<span class="body-compact-02 text-gray-60">
									({role.startedAt.toLocaleDateString('th-TH', {
										month: 'short',
										year: '2-digit'
									})}
									- {role.endedAt
										? role.endedAt.toLocaleDateString('th-TH', {
												month: 'short',
												year: '2-digit'
										  })
										: 'ปัจจุบัน'})
								</span>
							</li>
						{/each}
					</ul>
				</div>
			{/if}
			{#if partyCount > 0}
				<hr class="border-0 border-solid border-gray-20 border-t w-full m-0 box-border" />
				<div>
					<h3 class="heading-02">{partyCount} พรรคที่เคยสังกัด</h3>
					<ul class="flex flex-col gap-[2px] ml-8 list-disc">
						{#each Object.entries(parties) as [party, partyData] (party)}
							<PartyDetail {party} data={partyData} />
						{/each}
					</ul>
				</div>
			{/if}
		</Section>
		<Section id="votes" title="ประวัติการลงมติ">
			<Vote slot="icon" size="32" />
			<InlineNotification
				slot="header-extension"
				class="m-0 mt-1 min-w-0"
				lowContrast
				kind="info"
				subtitle="การประเมินพฤติกรรมการลงมติ จะพิจารณาเพียงชื่อมติไม่ได้ ควรศึกษาเนื้อหาของมตินั้นๆ ประกอบด้วย"
			/>
			<div class="flex flex-col gap-6">
				<div class="flex flex-col gap-2">
					<h3 class="body-02 px-2 py-1 bg-teal-50">
						5 มติล่าสุด ที่{politician.firstname}<span class="heading-02">เห็นด้วย</span>
					</h3>
					<!-- TODO: add links -->
					<ul class="flex flex-col gap-2 body-01 list-disc ml-8">
						{#each agreedVoting.latest as voting, idx (idx)}
							<li>
								<a class="flex items-start gap-1 text-black no-underline cursor-pointer" href="/">
									<span class="flex-1 max-w-max underline">{voting.title}</span>
									<VotingResultTag
										class="cursor-pointer m-0 whitespace-nowrap"
										result={voting.result}
									/>
								</a>
							</li>
						{/each}
					</ul>
					<a
						href="/politicians/{politician.id}/votes?votetype=agreed"
						class="mr-auto helper-text-01 flex gap-2 items-center"
						target="_blank"
						rel="nofollow noopener noreferrer"
					>
						<span>ดู {agreedVoting.total} มติที่เห็นด้วย</span>
						<ArrowRight />
					</a>
				</div>
				<div class="flex flex-col gap-2">
					<h3 class="body-02 px-2 py-1 bg-red-50 text-white">
						5 มติล่าสุด ที่{politician.firstname}<span class="heading-02">ไม่เห็นด้วย</span>
					</h3>
					<!-- TODO: add links -->
					<ul class="flex flex-col gap-2 body-01 list-disc ml-8">
						{#each disagreedVoting.latest as voting, idx (idx)}
							<li>
								<a class="flex items-start gap-1 text-black no-underline cursor-pointer" href="/">
									<span class="flex-1 max-w-max underline">{voting.title}</span>
									<VotingResultTag
										class="cursor-pointer m-0 whitespace-nowrap"
										result={voting.result}
									/>
								</a>
							</li>
						{/each}
					</ul>
					<a
						href="/politicians/{politician.id}/votes?votetype=disagreed"
						class="mr-auto helper-text-01 flex gap-2 items-center"
						target="_blank"
						rel="nofollow noopener noreferrer"
					>
						<span>ดู {disagreedVoting.total} มติที่ไม่เห็นด้วย</span>
						<ArrowRight />
					</a>
				</div>
				<div class="flex flex-col gap-2">
					<h3 class="body-02 px-2 py-1 bg-gray-20 heading-02">การลา/ขาดประชุม</h3>
					<p class="body-02">
						{politician.firstname}ลา/ขาดประชุมในการลงมติ {votingAbsentStats.absentVoting} มติ ({safePercent(
							votingAbsentStats.absentVoting,
							votingAbsentStats.totalVoting
						)}%) จากทั้งหมด
						{votingAbsentStats.totalVoting}
						มติในฐานข้อมูล ซึ่ง{votingAbsentStats.absentVoting ===
						votingAbsentStats.averageAbsentVoting
							? 'เท่ากับ'
							: votingAbsentStats.absentVoting < votingAbsentStats.averageAbsentVoting
							? 'น้อยกว่า'
							: 'มากกว่า'}ค่ากลางของสมาชิกในสภาทั้งหมด (ค่ากลาง = {safePercent(
							votingAbsentStats.averageAbsentVoting,
							votingAbsentStats.totalVoting
						)}%)
					</p>
					<p class="label-01 text-gray-60">
						หมายเหตุ: การขาดลงมติ เกิดจากหลายสาเหตุ เช่น ติดประชุมอื่น ติดภารกิจสำคัญ เจ็บป่วย
						จึงอาจไม่ได้สะท้อนความไม่รับผิดชอบเสมอไป
					</p>
					<a
						href="/politicians/{politician.id}/votes?votetype=absent"
						class="mr-auto helper-text-01 flex gap-2 items-center"
						target="_blank"
						rel="nofollow noopener noreferrer"
					>
						<span>ดู {votingAbsentStats.absentVoting} มติที่ขาด</span>
						<ArrowRight />
					</a>
				</div>
				<Button
					href="/politicians/{politician.id}/votes"
					kind="tertiary"
					icon={ArrowRight}
					size="small">ดูการลงมติทั้งหมด</Button
				>
			</div>
		</Section>
	</div>
</div>
