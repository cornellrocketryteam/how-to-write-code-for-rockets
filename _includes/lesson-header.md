<div class="card mb-2">
	<div class="card-body">
		<div class="row">
			<div class="col-md-4 col-sm-12 pb-2">
				<strong>Prerequisites</strong>
				{{include.prereqs | markdownify}}
			</div>
			<div class="col-md-4 col-sm-12 pb-2">
				<strong>Goals</strong>
				{{include.goals | markdownify}}
			</div>
			<div class="col-md-4 col-sm-12 pb-2">
				<strong>See also</strong>
				{{include.seealso | markdownify}}
			</div>
		</div>
	</div>
</div>